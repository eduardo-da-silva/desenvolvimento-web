## Criação de uma aplicação VueJS

!!!warning "Importante"

    Antes de iniciar a criação da aplicação, é importante que você tenha o NodeJS instalado e configurado em seu ambiente.

    - Garantir que os passos da [Aula inicial](../index.md#configurando-o-ambiente) foram executados.
    - Crie uma nova pasta para o seu projeto e abra no VSCode.
    - Abra a **pasta** do projeto no vscode (repita em voz alta: _"Nunca abra um arquivo, sempre abra a pasta."_).

Para criar uma aplicação VueJS, abra o terminal no diretório em que você deseja criar o projeto e execute o comando:

```bash
npm init vue@latest [nome-do-projeto]
```

_Note que usamos um parâmetro `[nome-do-projeto]` que é opcional. Se você informar este parâmetro, ele criará um projeto com o nome informado, caso contrário, ele solicitará o nome do projeto._

O comando anterior irá criar uma aplicação VueJS usando uma ferramenta de scaffolding chamada `create-vue`. Ele apresentará uma série de perguntas para você. Responda conforme a seguir:

1. **Project name**: informe o nome do projeto. Este nome será usado para criar a pasta do projeto.

2. **Select features to include in your project**: selecione as funcionalidades que você deseja incluir no projeto. Você pode navegar pelas opções usando as setas do teclado e selecionar/deselecionar as opções usando a barra de espaço. Abaixo, eu deixei um exemplo do que você deve pode escolher nesta etapa inicial do curso.

```bash
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

3. **Install Oxlint for faster linting**: selecione `No` para não instalar o Oxlint.

Então ele fará a criação do projeto em uma pasta com o nome do projeto informado.

Note que no exemplo anterior, escolhemos não usar o Vue Router, Pinia, Vitest, Cypress, ESLint e Prettier, bem como o suporte ao TypeScript e JSX. Você pode escolher o que desejar.

Agora, abra no VSCode a pasta do projeto criado. Importante que você abra a pasta do projeto, e não um arquivo específico. Outro ponto importante: caso você tenha executado o comando de criação do projeto já dentro do VS Code, eu sugiro que você reabra na pasta do projeto, pois o VS Code pode não reconhecer o projeto corretamente.

Em seguida, basta executar os seguintes comandos:

```bash
npm install
npm run dev
```

O primeiro comando instala as dependências do projeto. O segundo comando executa o servidor de desenvolvimento do VueJS. Em geral, o servidor estará em execução na porta 5173, caso esta esteja livre. Para acessar a aplicação, basta abrir o navegador e acessar a URL `http://localhost:5173`.

```bash
  VITE v6.2.2  ready in 500 ms

  ➜  Local:   http://127.0.0.1:5173/
  ➜  Network: use --host to expose
```

A imagem mostra a tela inicial da aplicação VueJS.

![Tela inicial da aplicação VueJS](../assets/CriacaoProjeto-TelaInicial.png)

!!!tip "Manter um repositório Git"

    É muito importante que logo após a criação do projeto você crie um repositório Git para o projeto. Para isso, você pode usar o próprio Visual Studio Code. Para isso, abra o menu `Source Control` e clique em `Initialize Repository`. Em seguida, clique em `Create Repository`. O Visual Studio Code irá criar um repositório Git na pasta do projeto. Isso requer que o usuário tenha o Git instalado e configurado. Para mais informações, consulte a [Aula inicial](../index.md#configurando-o-ambiente).

    Também, é importante que a cada alteração que você fizer no projeto, você faça um commit. Para isso, abra o menu `Source Control` e clique em `Stage All Changes`. Em seguida, clique em `Commit`. O Visual Studio Code irá criar um commit com as alterações realizadas. Para mais informações, consulte a [Aula inicial](../index.md#configurando-o-ambiente).

## Estrutura de arquivos

A imagem a seguir mostra a estrutura de arquivos inicial do projeto.

![Estrutura de arquivos do projeto](../assets/CriacaoProjeto-EstruturaArquivos.png)

Esta estrutura pode ser resumida da seguinte forma:

- `node_modules`: pasta com as dependências do projeto.
- `public`: pasta com os arquivos estáticos da aplicação.
- `src`: pasta com os arquivos fonte da aplicação. Por padrão, o arquivo `App.vue` é o componente raiz da aplicação, enquanto o arquivo `main.js` é o ponto de entrada da aplicação. Em geral, esta é a pasta que você irá trabalhar.
- `index.html`: arquivo raiz do projeto que define .
- `package.json`: arquivo com as configurações do projeto.
- `package-lock.json`: arquivo com as configurações de versões das dependências do projeto.
- `README.md`: arquivo com as instruções de instalação e execução do projeto.
- `vite.config.js`: arquivo com as configurações do servidor de desenvolvimento.

### O arquivo index.html

O arquivo `index.html` é o arquivo raiz da aplicação. Ele define o elemento raiz da aplicação, que é o elemento `<div id="app">`. Este elemento é o elemento que será substituído pelo VueJS. O arquivo `index.html` também define o arquivo `main.js` como o ponto de entrada da aplicação.

O código a seguir mostra o arquivo `index.html`:

```html title="index.html" linenums="1" hl_lines="7"
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

Em geral, você não precisará alterar este arquivo. Contudo, alguns ajustes podem ser realizados. Por exemplo, você pode alterar o título da página, na linha 7, conforme o código a seguir:

```html
<title>Aplicação exemplo Vue3</title>
```

Também, podem ser adicionados outras referências, como por exemplo, para um pacote de arquivos CSS.

Note também que antes de fechar a tag `</body>`, há uma referência para o arquivo `main.js`. Este arquivo é o ponto de entrada da aplicação.

### O arquivo main.js

Como comentando anteriormente, o arquivo `main.js` é o ponto de entrada da aplicação. Ele é responsável por carregar o VueJS e o componente raiz da aplicação. O código a seguir mostra o arquivo `main.js`:

```javascript title="./src/main.js" linenums="1"
import './assets/main.css';

import { createApp } from 'vue';
import App from './App.vue';

createApp(App).mount('#app');
```

Neste exemplo, o arquivo `main.js` importa o método `createApp` do pacote `vue`, responsável por criar a aplicação VueJS. Em seguida, o arquivo importa o componente raiz da aplicação, que é o arquivo `App.vue`. E, por fim, o arquivo importa o arquivo `main.css`, que é o arquivo de estilo da aplicação.

Na última linha, o arquivo chama o método `createApp` passando o componente raiz da aplicação como parâmetro. O método `createApp` retorna um objeto que possui o método `mount`, responsável por montar a aplicação no elemento raiz da aplicação, que é o elemento `<div id="app">`. A div com o id `app` é definida no arquivo `index.html`.

Ao longo das atividades, você irá alterar este arquivo para adicionar novos componentes e novas funcionalidades.

### O arquivo App.vue

O arquivo `App.vue` é o componente raiz da aplicação. Ele é responsável por carregar os demais componentes da aplicação. O código a seguir mostra a conteúdo padrão, que vem com a instalação, do arquivo `App.vue`:

```html title="./src/App.vue" linenums="1"
<script setup>
  import HelloWorld from './components/HelloWorld.vue';
  import TheWelcome from './components/TheWelcome.vue';
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
  header {
    line-height: 1.5;
  }

  .logo {
    display: block;
    margin: 0 auto 2rem;
  }

  @media (min-width: 1024px) {
    header {
      display: flex;
      place-items: center;
      padding-right: calc(var(--section-gap) / 2);
    }

    .logo {
      margin: 0 2rem 0 0;
    }

    header .wrapper {
      display: flex;
      place-items: flex-start;
      flex-wrap: wrap;
    }
  }
</style>
```

Neste momento, você não precisa entender o código deste arquivo. Contudo, é importante que você saiba que este é o componente raiz da aplicação. Inicialmente, ele carrega dois componentes: `HelloWorld` e `TheWelcome`. Estes componentes são definidos nos arquivos `HelloWorld.vue` e `TheWelcome.vue`, respectivamente, ambos na pasta `./src/components`.

Não nos deteremos neste arquivo, pois ele será alterado ao longo das atividades.
