# Tutorial Livraria (Carrinho de compras)

Nesta etapa, você irá desenvolver uma aplicação de carrinho de compras utilizando Vue.js. O objetivo é criar uma aplicação que permita ao usuário adicionar produtos a um carrinho, visualizar o carrinho e finalizar a compra.

Usaremos como base esse [protótipo](https://www.figma.com/design/iY248n1M3QOKwrtlWrZe9K/Exerc%C3%ADcios-LIvraria?node-id=0-1&p=f&t=KNgrCI6guO3oZ20n-0) feito no Figma. Neste momento, vamos fazer tudo usando apenas um componente, ou seja, apenas o arquivo `App.vue`. O objetivo é que você consiga entender como funciona a estrutura de uma aplicação Vue.js.

Vamos desenvolver a aplicação em etapas, começando com a configuração do ambiente e a criação da estrutura básica do projeto. Em seguida, adicionaremos os componentes necessários para o carrinho de compras e implementaremos a lógica de adição e remoção de produtos.

## Criando a aplicação

Para criar a aplicação, siga os passos abaixo (1):
{ .annotate }

1. Lembre-se que você deve estar com o Node na versão superior a 20.0.0 e estar num diretório adequado para criar o projeto.

```bash
npm init vue@latest tutorial-livraria
◆  Select features to include in your project: (↑/↓ to navigate, space to select, a to toggle all, enter to confirm)
│  ◻ TypeScript
│  ◻ JSX Support
│  ◻ Router (SPA development)
│  ◻ Pinia (state management)
│  ◻ Vitest (unit testing)
│  ◻ End-to-End Testing
│  ◼ ESLint (error prevention)
│  ◼ Prettier (code formatting)
```

Em seguida, abra a pasta `tutorial-livraria` no VSCode e execute os seguintes comandos no terminal:

```bash
npm install
npm run dev
```

Lembrando que, com os comandos acima, você instala as dependências do projeto e inicia o servidor de desenvolvimento. O servidor estará em execução na porta 5173, caso esta esteja livre. Para acessar a aplicação, basta abrir o navegador e acessar a URL `http://localhost:5173`.

Vamos agora fazer a limpeza do projeto:

- [x] Abra o arquivo `src/App.vue` e remova todo o conteúdo, deixando apenas a tag `<template>` e a tag `<script setup>`. O arquivo deve ficar assim:

```vue title="./src/App.vue" linenums="1"
<script setup></script>

<template></template>
```

- [x] Remova todos os arquivos e subdiretórios da pasta `src/components`.
- [x] Edite o arquivo `src/assets/main.css`, e deixe como abaixo:

  ```css title="./src/assets/main.css" linenums="1"
  @import './base.css';

  html {
    font-size: clamp(1rem, 1.5vw, 1.2rem);
    line-height: 1.5;
  }
  ```

Note que o arquivo `base.css` é um arquivo CSS que contém as regras de estilo base para a aplicação. Ele é importado no arquivo `main.css`, que é o arquivo principal de estilos da aplicação. Também removemos as regras de estilo que estavam no arquivo `main.css` e deixamos apenas as regras de estilo base e da tag `html`. Nesse caso, a regra de estilo `font-size` define o tamanho da fonte da aplicação. O valor `clamp(1rem, 1.5vw, 1.2rem)` significa que o tamanho da fonte será de 1rem (16px) no menor tamanho de tela, aumentará para 1.5vw (1.5% da largura da tela) em telas médias e será limitado a 1.2rem (19.2px) em telas grandes.

## Instalando o pacote de ícones

Para a criação desse projeto, usaremos a biblioteca de ícones [Material Design Icons](https://fonts.google.com/icons?icon.query=material%20design%20icons). Para instalar, execute o seguinte comando:

```bash
npm install @mdi/font #(1)(2)
```

1. Antes de executar esse comando, é aconselhável parar a execução do servidor de desenvolvimento. Para isso, pressione `Ctrl + C` no terminal onde o servidor está em execução. Isso interromperá o processo do servidor.
2. O comando acima instala a biblioteca de ícones Material Design Icons. Essa biblioteca contém uma coleção de ícones que podem ser usados em aplicações web. A biblioteca é baseada no Material Design, um sistema de design criado pelo Google.

Em seguida, vamos importar os ícones no arquivo `src/main.js`. Para isso, abra o arquivo `src/main.js` e adicione a seguinte linha:

```javascript title="./src/main.js" linenums="1" hl_lines="2"
import './assets/main.css';
import '@mdi/font/css/materialdesignicons.css';
```

???info ":eye::eye: Versão completa"

    ```javascript title="./src/main.js" linenums="1" hl_lines="2"
    import './assets/main.css'
    import '@mdi/font/css/materialdesignicons.min.css'

    import { createApp } from 'vue'
    import App from './App.vue'

    createApp(App).mount('#app')
    ```

Uma lista completa de ícones do Material Design Icons pode ser encontrada [aqui](https://pictogrammers.com/library/mdi/). A forma de usar os ícones é adicionar a classe correspondente ao elemento HTML desejado. Por exemplo, o ícone do carrinho é representado pela classe `mdi mdi-cart`. Para usar um ícone, basta adicionar a classe correspondente ao elemento HTML desejado. Em geral, os ícones são usados em elementos `<span>` ou `<i>`.

Também, para criar a aplicação, precisaremos das imagens que foram usadas no protótipo e que são as capas dos livros. Para isso, você pode baixar o arquivo de imagens, clicando no botão abaixo.

[Baixar arquivo de imagens :fontawesome-solid-download:](../assets/imagens.zip){ .md-button .md-button--primary }

--8<-- "docs/livraria-tutorial/header.md"
--8<-- "docs/livraria-tutorial/hero.md"
--8<-- "docs/livraria-tutorial/featured.md"
--8<-- "docs/livraria-tutorial/books.md"
--8<-- "docs/livraria-tutorial/footer.md"
--8<-- "docs/livraria-tutorial/cart.md"
--8<-- "docs/livraria-tutorial/handle-cart-items.md"

## Conclusão

Com esses passos concluídos, você terá uma aplicação básica de carrinho de compras em Vue.js. A aplicação possui um cabeçalho, uma seção de destaque, uma seção de livros e um rodapé. Além disso, a aplicação possui um carrinho de compras que permite adicionar e remover produtos.

Nas próximas aulas, vamos utilizar essa aplicação como base para implementar funcionalidades mais avançadas, como o uso de componentes, rotas, e gerenciamento de estado com o Pinia.
