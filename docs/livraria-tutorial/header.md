## Criando o cabeçalho

Vamos inicialmente criar a estrutura principal do cabeçalho, ainda sem a funcionalidade de abrir o carrinho. Para isso, vamos editar o arquivo `src/App.vue` e adicionar o seguinte código:

```vue title="./src/App.vue" linenums="4"
<template>
  <header>
    <nav>
      <h1>
        <a href="#">
          IFbooks
          <span class="logo-title"> Apreço a livros </span>
        </a>
      </h1>
      <div class="search-wrapper">
        <input type="text" class="search" placeholder="Buscar..." />
      </div>
      <ul>
        <li>Termos</li>
        <li>Equipe</li>
        <li>Envio</li>
        <li>Devoluções</li>
      </ul>
      <ul class="icons">
        <li><span class="mdi mdi-cart"></span></li>
        <li><span class="mdi mdi-heart"></span></li>
        <li><span class="mdi mdi-account"></span></li>
      </ul>
    </nav>
  </header>
</template>
```

Note, no código acima, os seguintes detalhes:

- O cabeçalho é composto por um `nav` que contém o título da aplicação, um campo de busca e uma lista de links.
- O cabeçalho também contém uma lista de ícones, que são representados por classes do Material Design Icons. Esses ícones são usados para representar ações como abrir o carrinho, visualizar favoritos e acessar a conta do usuário.
- Os ícones do Material Design Icons são representados por classes CSS. Por exemplo, o ícone do carrinho é representado pela classe `mdi mdi-cart`. Para usar um ícone, basta adicionar a classe correspondente ao elemento HTML desejado. Uma lista completa de ícones pode ser encontrada [aqui](https://pictogrammers.com/library/mdi/).
- O cabeçalho já possui várias classes definidas que facilitará a estilização. Em seguida vamos adicionar o CSS para estilizar o cabeçalho.
- O cabeçalho possui um link que leva à página inicial da aplicação. O link é representado pela tag `<a>` e contém o título da aplicação. O título é estilizado com a classe `logo-title`, que pode ser usada para aplicar estilos específicos ao título.
- O cabeçalho possui uma barra de pesquisa, que é representada pelo elemento `<input>`. A barra de pesquisa é estilizada com a classe `search`, que pode ser usada para aplicar estilos específicos à barra de pesquisa.
- O cabeçalho possui uma lista de links, que são representados pelos elementos `<li>`. Os links são estilizados com a classe `icons`, que pode ser usada para aplicar estilos específicos aos ícones.

Agora, vamos adicionar a estilização no próprio componente. Para isso, adicione o seguinte código no arquivo `src/App.vue`:

```vue title="./src/App.vue" linenums="33"
<style scoped>
header nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2vh 8vw;
  border-bottom: 2px solid #27ae6099;

  & h1 {
    font-size: 1.3rem;
    color: #000;

    & a {
      text-decoration: none;
      color: #000;
      display: flex;
      align-items: center;
    }

    & .logo-title {
      border-left: 1px solid #27ae6099;
      font-size: 0.8rem;
      margin-left: 10px;
      padding-left: 10px;
      color: #27ae6099;
      width: 100px;
      line-height: 1rem;
    }
  }

  & input {
    width: 400px;
    height: 40px;
    border-radius: 5px;
    font-size: 1rem;
    border: 0;
    background-color: #f1f1f1;
    padding: 5px;
  }

  & ul {
    display: flex;
  }

  & ul li {
    list-style: none;
    margin: 0 10px;
    font-size: 1rem;
  }

  & .icons li {
    color: #27ae60;
    font-size: 1.3rem;
  }

  & .search-wrapper {
    position: relative;
  }

  & .search-wrapper::before {
    content: '󰍉'; /* Code glyph para mdi-magnify */
    font-family: 'Material Design Icons';
    font-size: 1.2rem;
    position: absolute;
    right: 0.75rem;
    top: 50%;
    transform: translateY(-50%);
    pointer-events: none;
  }

  & .search {
    padding-right: 2rem;
  }
}
</style>
```

Note que o código acima utiliza uma característica do CSS chamado de `nesting`, que permite aninhar seletores CSS dentro de outros seletores. Isso torna o código mais legível e organizado. O `&` é um seletor especial que representa o elemento pai. Por exemplo, `& h1` representa o elemento `<h1>` dentro do elemento pai.

O código acima estiliza o cabeçalho da aplicação, definindo a aparência do título, da barra de pesquisa e dos ícones. O cabeçalho é exibido na parte superior da página e contém um link para a página inicial, uma barra de pesquisa e uma lista de ícones. A barra de pesquisa é estilizada com um fundo cinza claro e um tamanho fixo. Os ícones são exibidos em verde e têm um tamanho maior que o texto normal.

???info ":eye::eye: Versão completa"

    ```vue title="./src/App.vue" linenums="1"
    <script setup>
    </script>

    <template>
        <header>
            <nav>
            <h1>
                <a href="#">
                IFbooks
                <span class="logo-title"> Apreço a livros </span>
                </a>
            </h1>
            <div class="search-wrapper">
                <input type="text" class="search" placeholder="Buscar..." />
            </div>
            <ul>
                <li>Termos</li>
                <li>Equipe</li>
                <li>Envio</li>
                <li>Devoluções</li>
            </ul>
            <ul class="icons">
                <li><span class="mdi mdi-cart"></span></li>
                <li><span class="mdi mdi-heart"></span></li>
                <li><span class="mdi mdi-account"></span></li>
            </ul>
            </nav>
        </header>
    </template>

    <style scoped>
    header nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 2vh 8vw;
        border-bottom: 2px solid #27ae6099;

        & h1 {
            font-size: 1.3rem;
            color: #000;

            & a {
            text-decoration: none;
            color: #000;
            display: flex;
            align-items: center;
            }

            & .logo-title {
            border-left: 1px solid #27ae6099;
            font-size: 0.8rem;
            margin-left: 10px;
            padding-left: 10px;
            color: #27ae6099;
            width: 100px;
            line-height: 1rem;
            }
        }

        & input {
            width: 400px;
            height: 40px;
            border-radius: 5px;
            font-size: 1rem;
            border: 0;
            background-color: #f1f1f1;
            padding: 5px;
        }

        & ul {
            display: flex;
        }

        & ul li {
            list-style: none;
            margin: 0 10px;
            font-size: 1rem;
        }

        & .icons li {
            color: #27ae60;
            font-size: 1.3rem;
        }

        & .search-wrapper {
          position: relative;
        }

        & .search-wrapper::before {
          content: '󰍉'; /_ Code glyph para mdi-magnify _/
          font-family: 'Material Design Icons';
          font-size: 1.2rem;
          position: absolute;
          right: 0.75rem;
          top: 50%;
          transform: translateY(-50%);
          pointer-events: none;
        }

        & .search {
          padding-right: 2rem;
        }
    }
    </style>
    ```
