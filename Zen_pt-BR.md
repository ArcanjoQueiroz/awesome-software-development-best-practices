# Zen

1. Desenvolva código para produção.
2. Desenvolva focado no tratamento de exceções. Nem sempre as coisas dão certo.
3. O código é de todos. Então, não prejudique o seu "amiguinho" tanto no momento de troubleshooting (em produção) quanto na evolução do código.
4. Use design patterns da forma correta e quando fizer sentido. Não nomeie os design patterns/classes/etc de forma incorreta. 
5. Não desacople validações do código de negócio a menos que faça sentido. As validações são parte da regra de negócio e de início não vão ser substituídas em tempo de execução.
6. Use checkstyle/linters tanto no front-end quanto no back-end. Veja o item #3.
7. Pergunte quando tiver dúvidas. Discuta a solução a ser implementada. Veja o item #1.
8. Evite desenvolver software com libraries ou frameworks deprecated. Se isso acontecer, você vai ter que fazer upgrade algum dia.
9. Faça testes unitários quando fizer sentido. Eles têm que te ajudar, além de serem sua "rede de segurança". 
10. Faça testes integrados quando fizer sentido. Veja o item #9.
11. Performance também é importante.
12. Não repita a si mesmo. É o [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle. Use a [OOP](https://en.wikipedia.org/wiki/Object-oriented_programming) (Herança, Polimorfismo, etc) + [Design Patterns](https://en.wikipedia.org/wiki/Software_design_pattern) para não repetir código.
13. Use [alta coesão e baixo acoplamento](https://medium.com/clarityhub/low-coupling-high-cohesion-3610e35ac4a6).
14. Aprenda [Git](https://git-scm.com/) pela linha de comando. Saiba o que você está fazendo.
15. A estrutura de um projeto/serviço/módulo pequeno é diferente de um projeto/serviço/módulo grande. Cuidado.
16. Use [Maven modules](https://maven.apache.org/guides/mini/guide-multiple-modules.html) quando for necessário.
17. Desenvolva para [i18n](https://en.wikipedia.org/wiki/Internationalization_and_localization).
19. Mensagens de erro são extremamente importantes.
20. Aprenda a nomear bem o seus [métodos/classes/funções/objetos](https://medium.com/mindorks/how-to-write-clean-code-lessons-learnt-from-the-clean-code-robert-c-martin-9ffc7aef870c) etc.
21. Respeite a organização do projeto. Se tiver uma sugestão de mudança, comente, discuta. Toda melhoria é muito bem vinda, mas se manifeste.
22. Use interfaces quando for necessário. Não faz sentido uma interface para somente uma implementação. 
23. Leia o README.md. E também escreva o README.md.
24. Use o conceito de [divisão-e-conquista](https://en.wikipedia.org/wiki/Divide-and-conquer_algorithm) tanto para algoritmos quando para problemas.
25. Use o [KISS](https://en.wikipedia.org/wiki/KISS_principle).
26. Não projete ou desenvolva usando o [BDUF](https://www.knowledge21.com.br/blog/bduf/). Projete usando o [YAGNI](https://deviq.com/yagni/).
27. Evite criar métodos com mais de 4 ou 5 argumentos.
28. Evite criar/modificar classes com mais 500 linhas. Se existir, tem que ser refatorada. Veja regra #38.
29. Use imutabilidade tanto quanto for possível.
30. Lembre-se que o código também vai para a memória, não só os valores e objetos.
31. Logs são muito importantes, mas não devem poluir o output. Use os diferentes níveis de log no seu projeto.
32. Lembre-se que comunicação via rede não é algo imediato e sem limites. Existe o conceito de tráfego de pacotes de dados e de largura de banda também.
33. Aprenda algoritmo, estrutura de dados e complexidade de algoritmos. É importante.
34. Desenvolva de modo iterativo e incremental.
35. Faça o deploy em produção o mais cedo se possível.
36. Aplicações distribuídas são complexas. Evite o máximo possível, mas se for necesário faça a quebra.
37. Distribua os seus serviços seguindo as regras de negócio e não por organização técnica.
38. Use a [regra do escoteiro](https://deviq.com/boy-scout-rule/).
39. Use pull requests como uma forma de discutir o código e verificar problemas. E não como uma ferramenta só para merge de código com a branch de desenvolvimento. Dá até para fazer comentários nas linhas!
40. Aprenda a dizer [não](https://codingjourneyman.com/2014/09/04/the-clean-coder-saying-no/) quando for necessário.

