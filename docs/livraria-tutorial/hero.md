## A seção Hero

A seção Hero vai apresentar uma imagem e um texto que descreve o livro e autor do mês. Essa seção é uma parte importante do layout, pois é a primeira que os visitantes verão ao acessar a página. Neste momento faremos uma implementação simples, com um livro estático, mas que pode ser facilmente adaptada para receber dados dinâmicos.

Inicialmente, vamos editar o arquivo `src/App.vue` para adicionar a seção Hero. Para isso, adicione o seguinte código no arquivo `src/App.vue`, no bloco `<template>`:

```html title="./scr/App.vue" linenums="29"
<section class="hero">
  <div class="hero-content">
    <h3 class="outlined">Livro destaque</h3>
    <h2>Noc Ognia</h2>
    <p>
      Noc ognia é um romance de Erich-Emmanuel Schmitt, que narra a história de
      um homem que vive em um mundo onde as pessoas não podem mais sonhar. O
      livro é uma reflexão sobre a importância dos sonhos e da imaginação na
      vida humana. Erich-Emmanuel Schmitt é um autor francês conhecido por suas
      obras que exploram temas filosóficos e existenciais. Ele é um dos autores
      mais traduzidos da França e suas obras têm sido amplamente elogiadas pela
      crítica.
    </p>
    <button>Acessar página do livro</button>
  </div>
  <div class="hero-image">
    <img src="/imgs/hero.png" alt="Hero Image" />
  </div>
</section>
```

Note que o código acima adiciona uma nova seção chamada "hero" ao layout. Essa seção contém um título, uma descrição e uma imagem. O título e a descrição são estilizados com classes CSS específicas, que serão definidas a seguir.

A definição do estilo da seção Hero será feita no próprio componente. Para isso, adicione o seguinte código no arquivo `src/App.vue`, no bloco `<style>`:

```css title="./scr/App.vue" linenums="104"
.hero {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5vh 9vw;
  border-bottom: 2px solid #27ae6099;

  & h2 {
    color: #382c2c;
    font-size: 3rem;
    font-weight: 700;
  }

  & .hero-content {
    width: 50%;
    padding-right: 20px;
    font-weight: 400;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 20px;

    & h3.outlined {
      background-color: transparent;
      color: #27ae60;
      border: 2px solid #27ae60;
      padding: 15px 20px;
      border-radius: 5px;
      font-size: 1rem;
    }

    & button {
      margin-top: 20px;
    }

    p {
      width: 70%;
    }
  }

  & .hero-image {
    width: 50%;
    text-align: right;
    padding-right: 4vw;

    & img {
      max-width: 100%;
      height: auto;
    }
  }
}
```

Neste caso, foi adicionado um estilo para a seção Hero, que inclui um layout flexível para alinhar o conteúdo e a imagem. O título e a descrição também foram estilizados com cores e tamanhos de fonte específicos. Note que não deve ter sido excluído o código do cabeçalho, pois ele é necessário para a renderização correta da página.

No quadro abaixo, você pode ver como está, neste ponto, o arquivo `src/App.vue`.

???info ":eye::eye: Versão completa"

    ```vue title="./src/App.vue" linenums="1" hl_lines="29-44 104-154"
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
        <section class="hero">
            <div class="hero-content">
                <h2>Noc Ognia</h2>
                <p>
                    Noc ognia é um romance de Erich-Emmanuel Schmitt, que narra a história de um homem que vive
                    em um mundo onde as pessoas não podem mais sonhar. O livro é uma reflexão sobre a
                    importância dos sonhos e da imaginação na vida humana. Erich-Emmanuel Schmitt é um autor
                    francês conhecido por suas obras que exploram temas filosóficos e existenciais. Ele é um dos
                    autores mais traduzidos da França e suas obras têm sido amplamente elogiadas pela crítica.
                </p>
                <button>Acessar página do livro</button>
            </div>
            <div class="hero-image">
                <img src="/imgs/hero.png" alt="Hero Image" />
            </div>
        </section>
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
    }

    .hero {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 5vh 9vw;
        border-bottom: 2px solid #27ae6099;

        & h2 {
            color: #382c2c;
            font-size: 3rem;
            font-weight: 700;
        }

        & .hero-content {
            width: 50%;
            padding-right: 20px;
            font-weight: 400;
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            gap: 20px;

            & h3.outlined {
                background-color: transparent;
                color: #27ae60;
                border: 2px solid #27ae60;
                padding: 15px 20px;
                border-radius: 5px;
                font-size: 1rem;
            }

            & button {
                margin-top: 20px;
            }

            p {
                width: 70%;
            }
        }

        & .hero-image {
            width: 50%;
            text-align: right;
            padding-right: 4vw;

            & img {
                max-width: 100%;
                height: auto;
            }
        }
    }
    </style>
    ```
