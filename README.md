# Awesome Software Development Best Practices

## Handling Errors

Try to make the error handling in your applications simple. Error handling is as important as **happy path** in an application. Nobody wants to receive the same systemic error message with no meaningful information or a language specific strack trace. Here are some principles to adopt:

* Use the http code correctly. If a resource is not found, for example, return http 404 code. The same for invalid arguments in your API (400) or an internal server error (500).

* Send info about the error to the caller. Return a JSON (or another format of text if you prefer) only with a **code** (for the computers) and a **message** (for the humans [developers, end users, testers, ...]). Let me give an example:

```js
{ "code": "APP.001", "message": "There is no address for the given zip-code" } 
```
You can translate the code for a meaningful message to the final users or show the message text received from the server. It's up to you. Try to create a pattern for all microservices/systems error codes, for example, APP.001, where APP is the microservice/system name and 001 is the error number.
It's nice if you use i18n (internationalisation) for your messages through **Accept-Language** header. Remember, your **end user could be a developer** too. You can add args field in your JSON to send special parameters too.

```js
{ "code": "APP.002", "message": "There are {0} types of candies in your pocket. You need {1} to execute this functionality", "args": [ 5, 10 ] }
```

In conclusion, keep the messages simple. Avoid send more than these three fields (code, message and args) as response. And so many code translations too.


* Handle the basic error types. Try to handle errors like resource not found (404), invalid arguments (400), service unavailable (503), unexpected errors (500) and the business errors as well.

* Use mime-types and headers correctly. If you return a JSON, use Content-Type application/json, not text/plain. Developers will appreciate that. The same for headers, like an authorisation header (see AWS API for example), for example. This practice won't pollute the query params with system values, but remember, the default http headers character encoding is ASCII. For errors don't forget to verify the Content-Type before extract error code and messages as well.

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
        // I don't know how many items will have in the list
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

## Naming RESTFul resources

Generally, RESTFul resources are named using **nouns**, not verbs or adjectives. Try to use **plural form** to naming your resources (or be consistent about singular or plural form) and design the API for you clients and not for your data. Let me give some examples:

```sh
$ curl -X GET 'http://localhost:8080/service/customers/1234' # Get 1234 customer
```

Where /service is the application context path, /customers is a resource and /1234 is an ID of the customer.

Another example:

```sh
$ curl -X GET 'http://localhost:8080/service/customers/1234/orders/7' # Get Order 7 from customer 1234
```

Now, some anti-pattern examples (It is important too):

```sh
$ curl 'http://localhost:8080/service/customerServiceImpl/1234' # Java Service naming structure
$ curl 'http://localhost:8080/service/rs/customerServiceImpl/1234/find' # rs is redundant and find is a verb
$ curl 'http://localhost:8080/service/rs/customerServiceImpl/service/customer?id=1234' # normally query params are optional and the noun customer is repeated
$ curl 'http://localhost:8080/service/rs/customers/items/1234' # Is it 1234 an item or a customer?
```

Keep your RESTFul URLs **short** and **model by resources** in order to become easier to understand and to consume the API. Your clients will thank you. 

## Identifiers

Please, don’t expose important ids to the users (I mean the, end users) mainly if they are numeric. The user can easily guess another valid identifiers and access other users content if there aren’t any validations, for example. Here are:

- First, try to use alphanumeric identifiers like this:

```sh
$ curl ‘http://localhost:8080/service/accounts/5ad0e9b546e0fb00458c31d9’
```

Instead of:

```sh
$ curl ‘http://localhost:8080/service/accounts/27’
```

- Don’t forget the **authentication** and **authorisation** for your RESTful Web Services. In some languages you can create some type of interceptor (Servlet Filters, Spring Security Filters, CXF Interceptors, Express Middlewares, Python Decorators and so on) for your HTTP requests in order to verify the user identity and permission. OAuth2 is a good choice for authorisation too.

- The RESTful Web Service must retrieve some essential info (like a company id or an internal id) through a JWT passed by a HTTP Authorisation Header. Let me give an example:

```sh
$ curl -X GET -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ” http://localhost:8080/service/accounts/5ad0e9b546e0fb00458c31d9’
```
- The JWT should carry only essential data (like an ID). Additional data should be retrieved using these identifiers.
