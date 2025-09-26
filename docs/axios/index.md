# Uso do Axios

## Comunicação com APIs usando Axios

Em um projeto Vue.js, é comum a necessidade de comunicação com APIs para buscar ou enviar dados. Para facilitar essa comunicação, uma das bibliotecas mais populares é o `axios`. O `axios` é um cliente HTTP baseado em Promises que funciona tanto no navegador quanto no Node.js, permitindo realizar requisições HTTP de forma simples e eficiente.

Outras alternativas populares para comunicação com APIs incluem o `fetch`, que é uma API nativa do JavaScript para fazer requisições HTTP, e o `Vue Resource`, que é uma biblioteca específica para Vue.js, embora seja menos utilizada atualmente em comparação com o `axios`.

Nas nossas aulas, focaremos no uso do `axios` devido à sua simplicidade, flexibilidade e ampla adoção na comunidade JavaScript.

Também desenvolveremos um projeto prático consultando uma API pública do TMDB (The Movie Database) para buscar informações sobre filmes, o que nos permitirá aplicar os conceitos aprendidos de forma concreta.

Nos nossos projetos, instalaremos o axios usando o `npm`, como segue:

```bash
npm install axios
```

Outras formas de instalação podem ser encontradas na [documentação](https://axios-http.com/ptbr/docs/intro) da biblioteca.

--8<-- "docs/axios/exemplos-de-uso.md"
