## A seção Featured

Ne sequência, vamos implementar a seção Featured, que é uma seção que exibe informações sobre os livros mais vendidos, livros recomendados e frete grátis para SC. Essa seção será exibida logo abaixo da seção Hero.

Vamos ainda editar o arquivo `src/App.vue` e adicionar o seguinte código no bloco `<template>`, logo abaixo da seção Hero:

```html title="./src/App.vue" linenums="48"
    <section class="featured">
        <div>
            <span class="mdi mdi-truck"></span>
            <h2>Frete grátis para SC</h2>
        </div>
        <div>
            <span class="mdi mdi-star"></span>
            <h2>Livros recomendados</h2>
        </div>
        <div>
            <span class="mdi mdi-book-open-page-variant"></span>
            <h2>Mais vendidos</h2>
        </div>
    </section>
</main>
```

Note que é um código simples, que apenas exibe três informações. A seção é composta por três divs, cada uma contendo um ícone e um título. Os ícones são representados por classes do Material Design Icons.

Para estilizar a seção Featured, adicione o seguinte código no arquivo `src/App.vue`, no bloco `<style>`(1):
{.annotate}

1. Sugiro que você adicione o código CSS logo após a definição das informações da seção Hero, para facilitar a leitura do código.

```css title="./src/App.vue" linenums="192"
.featured {
  display: flex;
  padding: 3vh 8vw;
  border-bottom: 2px solid #27ae6099;

  & div {
    display: flex;
    align-items: center;
    flex: 1;
    justify-content: center;
    gap: 10px;

    & span {
      font-size: 2rem;
    }

    & h2 {
      font-size: 1.2rem;
      font-weight: 700;
    }
  }

  & article:nth-child(2) {
    border-left: 1px solid #27ae6099;
    border-right: 1px solid #27ae6099;
  }
}
```

No código acima, a seção Featured é estilizada para exibir três informações em uma linha. Cada informação é composta por um ícone e um título. A seção é dividida em três partes, cada uma ocupando um espaço igual na tela. A seção também possui uma borda inferior para separá-la da seção Hero.

No bloco abaixo está versão completa desenvolvida até aqui. Você pode comparar com o código que você desenvolveu até agora e verificar se está tudo certo.

???info ":eye::eye: Versão completa"

    ```vue title="./src/App.vue" linenums="1" hl_lines="48-61 192-218"
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
        <main>
            <section class="hero">
                <div class="hero-content">
                    <h3 class="outlined">Livro destaque</h3>
                    <h2>Noc Ognia</h2>
                    <p>
                        Noc ognia é um romance de Erich-Emmanuel Schmitt, que narra a história de um homem que
                        vive em um mundo onde as pessoas não podem mais sonhar. O livro é uma reflexão sobre a
                        importância dos sonhos e da imaginação na vida humana. Erich-Emmanuel Schmitt é um autor
                        francês conhecido por suas obras que exploram temas filosóficos e existenciais. Ele é um
                        dos autores mais traduzidos da França e suas obras têm sido amplamente elogiadas pela
                        crítica.
                    </p>
                    <button>Acessar página do livro</button>
                </div>
                <div class="hero-image">
                    <img src="/hero.png" alt="Hero Image" />
                </div>
            </section>
            <section class="featured">
                <div>
                    <span class="mdi mdi-truck"></span>
                    <h2>Frete grátis para SC</h2>
                </div>
                <div>
                    <span class="mdi mdi-star"></span>
                    <h2>Livros recomendados</h2>
                </div>
                <div>
                    <span class="mdi mdi-book-open-page-variant"></span>
                    <h2>Mais vendidos</h2>
                </div>
            </section>
        </main>
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

    .featured {
        display: flex;
        padding: 3vh 8vw;
        border-bottom: 2px solid #27ae6099;

        & div {
            display: flex;
            align-items: center;
            flex: 1;
            justify-content: center;
            gap: 10px;

            & span {
                font-size: 2rem;
            }

            & h2 {
                font-size: 1.2rem;
                font-weight: 700;
            }
        }

        & article:nth-child(2) {
            border-left: 1px solid #27ae6099;
            border-right: 1px solid #27ae6099;
        }
    }

    button {
        background-color: #27ae60;
        color: #fff;
        border: none;
        padding: 15px 20px;
        border-radius: 5px;
        font-size: 1rem;
        cursor: pointer;
        gap: 20px;
        display: flex;
        justify-content: center;

        &.outlined {
            background-color: transparent;
            color: #27ae60;
            border: 2px solid #27ae60;
        }

        &.plain {
            background-color: transparent;
            color: black;
            border: none;
            cursor: pointer;
        }
    }
    </style>
    ```
