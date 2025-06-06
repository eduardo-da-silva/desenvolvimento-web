# Roteamento

## Conceitos de roteamento

Quando desenvolvemos aplicações web, é comum que elas tenham mais de uma página. Para facilitar a navegação entre essas páginas, utilizamos o conceito de roteamento. O roteamento é o processo de determinar qual conteúdo deve ser exibido em uma página web com base na URL acessada pelo usuário.

Vale lembrar que quando usamos o VueJS estamos desenvolvendo uma Single Page Application (SPA), ou seja, uma aplicação web que carrega uma única página HTML e atualiza o conteúdo dinamicamente, sem a necessidade de recarregar a página. O roteamento em uma SPA é feito de forma dinâmica, sem a necessidade de recarregar a página.

No VueJS, o roteamento é feito com o Vue Router, uma biblioteca oficial que nos permite adicionar rotas à nossa aplicação. Com o Vue Router, podemos definir diferentes rotas para a nossa aplicação e associar cada rota a um componente específico. Dessa forma, quando o usuário acessa uma determinada URL, o Vue Router carrega o componente correspondente e exibe o conteúdo na página.

Neste capítulo, vamos aprender a utilizar o Vue Router para adicionar rotas à nossa aplicação VueJS. Vamos criar um projeto VueJS com o Vue Router e adicionar rotas para diferentes páginas. Além disso, vamos aprender a navegar entre as páginas da aplicação e a passar parâmetros para as rotas.

--8<-- "docs/router/basic.md"
--8<-- "docs/router/dynamic.md"
--8<-- "docs/router/programmatic.md"
