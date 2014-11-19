---
title: Perguntas frequentes sobre Gendarme (FAQ)
redirect_from:
  - /Gendarme.Development.FAQ/
---

Geral
=======

Posso ter minhas regras privadas no Gendarme?
--------------------------------------------

Claro. Desde o início o [Gendarme](/docs/tools+libraries/tools/gendarme/) framework foi projetado para esse propósito. [Gendarme](/docs/tools+libraries/tools/gendarme/) permite que as regreas fiquem separadas do Framework (e runners) lógica para garantir que este cenário será sempre funcione.

Posso usar algo diferente de C# para escrever regras?
---------------------------------------------------

Sim pode. No entanto, essas regras tem uma pequena chance de serem aceitas pelo [Gendarme](/docs/tools+libraries/tools/gendarme/) desde as dependências (por exemplo, o compilador) acrescentaria uma carga para o pacote pai, **mono-tools**, e o tornaria dificil de construir o pacote.

Quando eu deveria escrever uma engine?
-------------------------------

Talvez nunca :-) Sério, engines nascem partindo da frustração de escrever **muitas** regras e encontrando muitas duplicações dentro delas. Mesmo assim, temos que garantir que a engine, em circunstâncias normais, forneçam um ganho considerável (por exemplo, o desempenho) sobre a duplicação existente. Outra solução (mais simples) para resolver o mesmo problema seria utilizar Helpers ou Rocks (ou seja, métodos de extenção).

Onde posso fazer perguntas técnicas sobre Gendarme?
----------------------------------------------------

Muitos desenvolvedores [Gendarme](/docs/tools+libraries/tools/gendarme/) estão no [IRC](/community/help/irc/), **#gendarme** no canal **GimpNET**. Você também pode se juntar ao [Grupo do Google Gendarme](http://groups.google.com/group/gendarme?hl=pt-br) e enviar suas perguntas para uma lista de emails.

Se suas pergunta estão relacionadas ao [Cecil](/docs/tools+libraries/libraries/Mono.Cecil/) então você deve enviá-las para o [Google group Cecil](http://groups.google.com/group/mono-cecil?hl=pt-br).

Building
========

Como posso criar o Gendarme?
--------------------------

Existem várias maneiras. A principal e totalmente suportada, é utilizando o Makefile.

Makefiles Por quê?
---------------

-   Porque é quase universal;
-   Porque o [Gendarme](/docs/tools+libraries/tools/gendarme/) precisa existir dentro do **mono-tools** e utilizar os pacotes de várias distribuiçoes Linux.
-   Porque é a única configuração que é automáticamente testada pelo **monobuild** (nossos bots de Integração contínua).

Qual a versão do Mono é necessária?
-----------------------------------

A mesma versão do Gendarme, ou seja, se você for utilizar o Gendarme 2.2 será necessário o Mono 2.2. É provável que as versões mais antigas funcione, mas não é garantido. 

Posso usar MonoDevelop para criar o Gendarme?
-----------------------------------------

Sim. Uma solução e um projeto com o [MonoDevelop](http://www.monodevelop.org) estão disponíveis em nosso [Repositório de Código](/community/contributing/source-code-repository/). Entretando, este **não** é o único mecanismo de construção a ser utilizado, pois é bem provável que alguns arquivos (regras e testes) possam estar faltando. Ou seja, você poderá ter que ajustar sua Solução/Projeto para fazê-lo funcionar.

Posso utilizar o Visual Studio para criar o Gendarme?
-------------------------------------------

Sim, mas você vai precisar de um VS.NET 2010 (ou anterior), para compilar a solução (um compilaor C# 4 é **necessário**). Nota-se que assim como o [MonoDevelop](http://www.monodevelop.org), estão disponíveis uma solução e um projeto em nosso [Repositório de Código](/community/contributing/source-code-repository/) que podem estar desatualizados (por exemplo, faltando alguns arquivos).

Contribuição
==========

Como faço para contribuir com uma nova regra?
How can I contribute a new rule ?
---------------------------------

1.  Define your idea, i.e. what the rule is about.
2.  *(optional but recommended)* Send an email to [Gendarme Google group](http://groups.google.com/group/gendarme) to solicit feedback and comments. You can go ahead while waiting for feedback.
3.  Develop the rule. We recommend writing the "core" unit tests before the rule.
4.  Test the rule
    1.  against your unit tests
    2.  against defects that Gendarme can find in your rule (*aka* `make self-test`)
    3.  against a large chunk of code (e.g. Mono 2.0 class libraries)

5.  Fix failures (i.e. things that should be reported as defects) and false positives (i.e. things that should not be reported as defects)
6.  Create a patch (unified diff) and sent it to the [Gendarme Google group](http://groups.google.com/group/gendarme) for review. This patch should include:
    1.  The source code for the new rule, including its documentation (XML doc in source)
    2.  The unit tests
    3.  Makefile integration (it should simply be adding the 2 files to Makefile.am)
    4.  ChangeLog entries (for both the rule and tests)

Can I use C# 3 ?
-----------------

Yes, [Gendarme](/docs/tools+libraries/tools/gendarme/) already use C# 3 features like extension methods and LINQ. This is not a problem since Mono support it\* and [Gendarme](/docs/tools+libraries/tools/gendarme/) can requires the (released) Fx 3.5 for Windows users. \*unless there is a known issue that makes the code incompatible between Mono and MS runtimes.

Can I use C# 4 ?
-----------------

Yes, starting with version 2.11 [Gendarme](/docs/tools+libraries/tools/gendarme/) can use C#4 features as long as the new Mono C# compiler (mcs) support them. Just like C# 3 (or any other features) it is important to be able to build [Gendarme](/docs/tools+libraries/tools/gendarme/), for both testing and packaging, on the two .NET runtimes.


