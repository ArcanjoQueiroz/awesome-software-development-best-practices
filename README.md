# Awesome Software Development Best Practices

## Handling errors

Try to make the error handling in your applications simple. Error handling is as important as **happy path** in an application. Nobody wants to receive the same systemic error message with no meaningful information or a language specific strack trace. Here are some principles to adopt:

* Use the http code correctly. If a resource is not found, for example, return http 404 code. The same for invalid arguments in your API (400) or an internal server error (500).

* Send info about the error to the caller. Return a JSON (or another format of text if you prefer) only with a **code** (for the computers) and a **message** (for the humans). Let me give an example:

```js
{ "code": "APP.001", "message": "There is no address for the given zip-code" } 
```
You can translate the code for a meaningful message to the users or show the message text received from the server. It's up to you. Try to create a pattern for all the microservices/systems error codes, for example, APP.001, where APP is the microservice/system name and 001 is the error number.
It's nice if you use i18n (internationalisation) for your messages through **Accept-Language** header.

* Handle the basic error types. Try to handle errors like resource not found, invalid arguments, service unavailable, unexpected errors and the business errors as well.

* Use mime-types and headers correctly. If you return a JSON use Content-Type application/json, not text/plain. Front-end developers will appreciate that. The same for headers, like an authorisation header (see AWS API for example), for example. This practice won't pollute the query params with systemic values, but remember, the default http headers character encoding is ASCII.

## Logging

Logging is important to see the application state in a specific period of time or execution of a functionality. There are lots of logging frameworks for different programming languages like Logback and Log4j for Java, Winston for Node.js and built-in logging module for Python, for example. The Spring Boot comes already with a logging framework (and you can change too) but the framework itself does nothing if the programmer doesn't know how to use. Let's see:

* Use logging level wisely. Don't put all messages as logging level INFO. Try to put other logging levels such as WARN and DEBUG.
* Change the logging level on the fly. It's good if you can change the logging level from INFO to DEBUG without restart the application. 
* Change the logging level of only specific packages or modules. Spring Boot can do that:
```java
-Dlogging.level.com.company.myproject=DEBUG
```
* Verify if the application log show meaningful information.
* Too many log may slow the application. Don't do that:

```java
list.stream()
    .forEach(x -> {
        // TODO doing something here
        // I don't know how many items will have in the list, it is dynamically
        logger.info("X-force: '{}'", x);
    });
```

* For Java developers. Try this:

```java
logger.debug("Initialising functionality with Deadpool: '{}', bar: '{}' and xpto: '{}'", foo, bar, xpto);
```
Instead of:

```java
if (logger.isDebugEnabled()) {
    logger.debug("Initialising functionality with Deadpool: '" + foo + "', bar: '" + bar + "' and xpto: '" + xpto + "'");
}
```
