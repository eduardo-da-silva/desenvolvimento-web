## Manipulando eventos

A manipulação de eventos é uma parte importante da programação de interfaces de usuário. No Vue.js, os componentes filhos podem emitir eventos que são capturados pelos componentes pais. Para isso, é necessário utilizar a diretiva v-on no componente pai e o método $emit no componente filho.

Vamos fazer um exemplo na criação do componente de cabeçalho. O cabeçalho da aplicação terá um ícone (`mdi-cart`) que, quando clicado, irá emitir um evento para o componente pai, que permitirá alternar entre a exibição e ocultação do carrinho de compras.

### Componente de cabeçalho

Primeiramente, vamos criar o componente de cabeçalho. Para isso, crie um novo arquivo chamado `HeaderComponent.vue` na pasta `src/components`. O conteúdo do arquivo deve ser o seguinte:

```vue title="./src/components/HeaderComponent.vue" linenums="1" hl_lines="2 24"
<script setup>
defineEmits(['click-cart']);
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
        <li @click="$emit('click-cart')"><span class="mdi mdi-cart"></span></li>
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

Note que, como nos casos anteriores, os blocos template e style foram praticamente copiados integralmente do arquivo `App.vue`. O que muda é que definimos um bloco `script`, onde declaramos o evento `click-cart` que será emitido quando o ícone do carrinho for clicado. Também, no bloco `template`, alteramos a linha 24 para adicionar o evento `click` no ícone do carrinho, que irá emitir o evento `click-cart` para o componente pai.

Agora, precisamos importar o componente `HeaderComponent` no arquivo `App.vue` e adicionar o evento `click-cart` no cabeçalho. Para isso, abra o arquivo `src/App.vue` e faça as seguintes alterações:

```vue title="./src/App.vue" linenums="1" hl_lines="7"
<script setup>
import { ref } from 'vue'

import FooterComponent from '@/components/FooterComponent.vue'
import HeroBanner from '@/components/HeroBanner.vue'
import FeaturedComponent from '@/components/FeaturedComponent.vue'
import HeaderComponent from '@/components/HeaderComponent.vue'
...
</script>
```

Também, precisamos editar o bloco `template` do arquivo `App.vue` para adicionar o evento `click-cart` no cabeçalho. Para isso, altere a linha 12 do arquivo `App.vue` para:

```vue title="./src/App.vue" linenums="75" hl_lines="2"
<template>
  <header-component @click-cart="showCart = !showCart" />
  <main v-if="showCart">
  ...
</template>
```

A versão completa do arquivo `App.vue` está no bloco abaixo.

???info ":eye::eye: Versão completa"

    Note que, além das linhas destacadas, foi retirado o código das tags `<section>` relativas ao _hero_ e _featured_ do arquivo `App.vue`. Também, foi removida a parte correspondente no bloco de `<style>`.

    ```vue title="./src/App.vue" linenums="1" hl_lines="7 76"
    <script setup>
    import { ref } from 'vue'

    import FooterComponent from '@/components/FooterComponent.vue'
    import HeroBanner from '@/components/HeroBanner.vue'
    import FeaturedComponent from '@/components/FeaturedComponent.vue'
    import HeaderComponent from '@/components/HeaderComponent.vue'

    const showCart = ref(false)
    const cart = ref({
        items: [],
        total: 0,
    })

    const books = [
        {
        id: 1,
        title: 'Comigo na livraria',
        cover: '/covers/comigo-na-livraria.png',
        price: 23.24,
        author: 'Martha Medeiros',
        },
        {
        id: 2,
        title: 'Quincas Borba',
        cover: '/covers/quincas-borba.png',
        price: 23.24,
        author: 'Machado de Assis',
        },
        {
        id: 3,
        title: 'A livraria',
        cover: '/covers/a-livraria.png',
        price: 13.94,
        author: 'Penelope Fitzgerald',
        },
        {
        id: 4,
        title: 'A hora da estrela',
        cover: '/covers/a-hora-da-estrela.png',
        price: 16.84,
        author: 'Clarice Lispector',
        },
        {
        id: 5,
        title: 'O alienista',
        cover: '/covers/o-alienista.png',
        price: 266.92,
        author: 'Machado de Assis',
        },
        {
        id: 6,
        title: 'Mar morto',
        cover: '/covers/mar-morto.png',
        price: 13.95,
        author: 'Jorge Amado',
        },
        {
        id: 7,
        title: 'Grande sertão',
        cover: '/covers/grande-sertao-veredas.png',
        price: 26.04,
        author: 'Guimarães Rosa',
        },
        {
        id: 8,
        title: 'Flor de poemas',
        cover: '/covers/flor-de-poema.png',
        price: 15.81,
        author: 'Cecília Meireles',
        },
    ]
    </script>

    <template>
      <header-component @click-cart="showCart = !showCart" />
      <main v-if="showCart">
        <section class="cart">
          <h2>Carrinho</h2>
          <table>
            <thead>
              <tr>
                <th>Título</th>
                <th>Quantidade</th>
                <th>Subtotal</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="book in cart.items" :key="book.id">
                <td class="cart-item">
                  <img :src="book.cover" :alt="book.title" />
                  <div class="cart-item-info">
                    <p class="cart-item-title">{{ book.title }}</p>
                    <p class="cart-item-author">{{ book.author }}</p>
                    <p class="cart-item-price">R$ {{ book.price.toFixed(2) }}</p>
                  </div>
                </td>
                <td>
                  <div class="cart-item-quantity">
                    <button class="plain">
                      <span class="mdi mdi-minus" />
                    </button>
                    {{ book.quantity }}
                    <button class="plain">
                      <span class="mdi mdi-plus" />
                    </button>
                  </div>
                </td>
                <td class="cart-item-subtotal">R$ {{ book.price * book.quantity }}</td>
              </tr>
            </tbody>
          </table>
          <button @click="showCart = false" class="outlined">Voltar para loja</button>
          <div class="cart-summary">
            <div class="cupom">
              <input type="text" placeholder="Código do cupom" />
              <button>Inserir cupom</button>
            </div>
            <div class="summary">
              <h2>Total da Compra</h2>
              <div class="summary-items">
                <span>Produtos</span> <span>R$ {{ cart.total.toFixed(2) }}</span> <span>Frete</span>
                <span> Grátis</span> <span>Total</span> <span>R$ {{ cart.total.toFixed(2) }}</span>
              </div>
              <button>Ir para pagamento</button>
            </div>
          </div>
        </section>
      </main>
      <main v-else>
        <hero-banner />
        <featured-component />
        <section class="books">
          <article class="book" v-for="book in books" :key="book.id">
            <img :src="book.cover" :alt="book.title" />
            <h2>{{ book.title }}</h2>
            <p class="book-author">{{ book.author }}</p>
            <span class="price-and-like">
              <p class="book-price">R$ {{ book.price.toFixed(2) }}</p>
              <span class="mdi mdi-heart-outline"></span>
            </span>
            <button><span class="mdi mdi-cart"></span>Comprar</button>
          </article>
        </section>
      </main>
      <footer-component />
    </template>

    <style scoped>
    .books {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      padding: 5vh 8vw;

      & .book {
        display: flex;
        flex-direction: column;
        min-width: 300px;
        width: calc(100% / 4 - 42px);
        margin: 20px;

        & h2 {
          font-size: 1.5rem;
          font-weight: 700;
        }

        & .book-author {
          font-size: 1rem;
        }

        & .book-price {
          font-size: 1.2rem;
          font-weight: 700;
        }

        & .price-and-like {
          display: flex;
          justify-content: space-between;
          margin-bottom: 20px;

          & .mdi-heart-outline {
            font-size: 1.3rem;
            color: #27ae60;
          }
        }
      }
    }

    .cart {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: center;
      padding: 5vh 8vw;
      border-bottom: 2px solid #27ae6099;

      & h2 {
        font-size: 2rem;
        font-weight: 700;
        color: #27ae60;
      }

      & table {
        width: 100%;
        border-collapse: collapse;
        margin: 40px 0;

        & th,
        td {
          padding: 10px;
          text-align: left;
        }

        & th {
          border-bottom: 2px solid #27ae6099;
          font-size: 1.2rem;
          font-weight: 700;
        }

        & td {
          border-bottom: 1px solid rgb(128, 128, 128);
          font-size: 1rem;
        }

        & .cart-item-quantity {
          display: flex;
          align-items: center;
        }

        & .cart-item-subtotal {
          font-size: 1.1rem;
          font-weight: 700;
        }

        & .cart-item {
          display: flex;
          align-items: center;
          gap: 20px;

          & img {
            width: 80px;
            height: auto;
          }

          & .cart-item-info {
            display: flex;
            flex-direction: column;
            gap: 5px;

            & .cart-item-title {
              font-size: 1.2rem;
              font-weight: 700;
            }
            & .cart-item-author {
              font-size: 1rem;
            }
            & .cart-item-price {
              font-size: 1.1rem;
              font-weight: 600;
            }
          }
        }
      }

      & .cart-summary {
        display: flex;
        justify-content: space-between;
        width: 100%;

        & .cupom {
          display: flex;
          align-items: center;
          margin-top: 80px;
          gap: 10px;

          & input {
            width: 350px;
            height: 50px;
            border-radius: 5px;
            font-size: 1rem;
            border: 2px solid rgb(128, 128, 128);
            padding: 5px;
          }
        }

        & .summary {
          border: 1px solid rgb(128, 128, 128);
          padding: 1vw;

          & h2 {
            font-size: 1.2rem;
            font-weight: 700;
            color: black;
          }

          & .summary-items {
            display: grid;
            grid-template-columns: 3fr 1fr;

            & span {
              padding: 10px 0;
              border-bottom: 1px solid rgb(128, 128, 128);
            }
          }

          & button {
            margin-top: 20px;
          }
        }
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
