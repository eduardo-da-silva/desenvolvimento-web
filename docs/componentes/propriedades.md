## Propriedades de um componente

Ao criar um componente, é possível passar propriedades para ele. As propriedades são valores que podem ser utilizados pelo componente para alterar seu comportamento ou sua aparência. As propriedades são passadas para o componente como atributos HTML e são acessadas pelo componente como variáveis JavaScript.

Para isso, como no caso dos eventos, elas precisam ser declaradas no componente. Para declarar uma propriedade, usamos a função `defineProps` do VueJS, que deve ser chamada dentro do bloco `<script setup>`, que é o bloco onde declaramos as variáveis e funções do componente.

### Componente do carrinho

Para exemplificar o uso de propriedades, vamos criar um componente que representa o carrinho de compras. Esse componente vai receber a propriedade: `cart` que é um objeto que contém um array com os itens do carrinho e o total do carrinho. O componente vai exibir a lista de itens do carrinho e o total do carrinho. O componente vai ser usado na página principal da livraria, onde vamos exibir o carrinho de compras.

Para isso, vamos criar o componente `CartComponent.vue` dentro da pasta `src/components`. O arquivo deve ficar assim:

```vue title="./src/components/CartComponent.vue" linenums="1" hl_lines="2 17"
<script setup>
defineProps(['cart']);
</script>

<template>
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
          <td class="cart-item-subtotal">
            R$ {{ book.price * book.quantity }}
          </td>
        </tr>
      </tbody>
    </table>
    <button class="outlined">Voltar para loja</button>
    <div class="cart-summary">
      <div class="cupom">
        <input type="text" placeholder="Código do cupom" />
        <button>Inserir cupom</button>
      </div>
      <div class="summary">
        <h2>Total da Compra</h2>
        <div class="summary-items">
          <span>Produtos</span> <span>R$ {{ cart.total.toFixed(2) }}</span>
          <span>Frete</span> <span> Grátis</span> <span>Total</span>
          <span>R$ {{ cart.total.toFixed(2) }}</span>
        </div>
        <button>Ir para pagamento</button>
      </div>
    </div>
  </section>
</template>

<style scoped>
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
</style>
```

Agora, temos que importar e usar o componente `CartComponent` no arquivo `src/App.vue`. Para isso, abra o arquivo `src/App.vue` e adicione o seguinte código:

```vue title="./src/App.vue" linenums="1" hl_lines="8"
<script setup>
import { ref } from 'vue'

import FooterComponent from '@/components/FooterComponent.vue'
import HeroBanner from '@/components/HeroBanner.vue'
import FeaturedComponent from '@/components/FeaturedComponent.vue'
import HeaderComponent from '@/components/HeaderComponent.vue'
import CartComponent from '@/components/CartComponent.vue'
...
</script>
```

Também, adicione o componente `CartComponent` no template do arquivo `src/App.vue`, como no código abaixo:

```vue title="./src/App.vue" linenums="78" hl_lines="2"
<main v-if="showCart"> 
  <cart-component :cart="cart"/>
</main>
```

Note que que na linha 79 o `CardComponent` foi adicionado dentro do bloco `<main>` que exibe o carrinho de compras. O componente `CartComponent` recebe a propriedade `cart`, que é um objeto que contém os itens do carrinho e o total do carrinho. Veja que o valor da propriedade `cart` foi enviado via diretiva `v-bind`, que é a forma de passar propriedades para um componente no VueJS. A diretiva `v-bind`, neste caso, foi abreviada para `:`. Assim, o valor da propriedade `cart` é o objeto `cart` que foi declarado no bloco `<script setup>`.

A versão completa do arquivo `App.vue` está no bloco abaixo.

???info ":eye::eye: Versão completa"

    Note que, além das linhas destacadas, foi retirado o código das tags `<section>` relativas ao _hero_ e _featured_ do arquivo `App.vue`. Também, foi removida a parte correspondente no bloco de `<style>`.

    ```vue title="./src/App.vue" linenums="1" hl_lines="8 79"
    <script setup>
    import { ref } from 'vue'

    import FooterComponent from '@/components/FooterComponent.vue'
    import HeroBanner from '@/components/HeroBanner.vue'
    import FeaturedComponent from '@/components/FeaturedComponent.vue'
    import HeaderComponent from '@/components/HeaderComponent.vue'
    import CartComponent from '@/components/CartComponent.vue'

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
        <cart-component :cart="cart"/>
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

### Melhorias no componente carrinho

Agora que temos o componente `CartComponent` funcionando, podemos fazer algumas melhorias nele. Vamos adicionar a funcionalidade de adicionar e remover itens do carrinho, e também habilitar o botão de "Voltar para a loja". Para isso, vamos criar três eventos no componente `CartComponent`:

- `increment-book`: evento que é emitido quando o usuário clica no botão de adicionar item ao carrinho. Esse evento deve passar o item que foi adicionado ao carrinho.
- `decrement-book`: evento que é emitido quando o usuário clica no botão de remover item do carrinho. Esse evento deve passar o item que foi removido do carrinho.
- `hide-cart`: evento que é emitido quando o usuário clica no botão de "Voltar para a loja". Esse evento não deve passar nenhum dado.

Para isso, vamos editar o componente `CartComponent.vue` e adicionar os eventos. O arquivo deve ficar assim:

```vue title="./src/components/CartComponent.vue" linenums="1" hl_lines="3 29 33 44"
<script setup>
defineProps(['cart']);
defineEmits(['hide-cart', 'increment-book', 'decrement-book']);
</script>

<template>
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
              <button @click="decrementBookToCart(book)" class="plain">
                <span class="mdi mdi-minus" />
              </button>
              {{ book.quantity }}
              <button @click="$emit('increment-book', book)" class="plain">
                <span class="mdi mdi-plus" />
              </button>
            </div>
          </td>
          <td class="cart-item-subtotal">
            R$ {{ book.price * book.quantity }}
          </td>
        </tr>
      </tbody>
    </table>
    <button @click="$emit('hide-cart')" class="outlined">
      Voltar para loja
    </button>
    <div class="cart-summary">
      <div class="cupom">
        <input type="text" placeholder="Código do cupom" />
        <button>Inserir cupom</button>
      </div>
      <div class="summary">
        <h2>Total da Compra</h2>
        <div class="summary-items">
          <span>Produtos</span> <span>R$ {{ cart.total.toFixed(2) }}</span>
          <span>Frete</span> <span> Grátis</span> <span>Total</span>
          <span>R$ {{ cart.total.toFixed(2) }}</span>
        </div>
        <button>Ir para pagamento</button>
      </div>
    </div>
  </section>
</template>

<style scoped>
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
</style>
```

Com isso, como já vimos anteriormente, o componente `CartComponent` emite os eventos `increment-book`, `decrement-book` e `hide-cart`. O evento `increment-book` é emitido quando o usuário clica no botão de adicionar item ao carrinho. O evento `decrement-book` é emitido quando o usuário clica no botão de remover item do carrinho. O evento `hide-cart` é emitido quando o usuário clica no botão de "Voltar para a loja". Esses eventos são usados para atualizar o estado do carrinho na aplicação.

Contudo, note que os eventos `increment-book` e `decrement-book` recebem também o item que foi adicionado ou removido do carrinho. Tal parâmetro é passado para o evento, e pode ser acessado no componente pai. Assim, podemos usar esses eventos para atualizar o estado do carrinho na aplicação.

Agora, vamos editar o arquivo `src/App.vue` e adicionar os métodos que vão lidar com os eventos emitidos pelo componente `CartComponent`. O arquivo deve ficar assim:

```vue title="./src/App.vue" linenums="78" hl_lines="2-7"
<main v-if="showCart"> 
  <cart-component 
    :cart="cart"
    @hide-cart="showCart = false"
    @increment-book="incrementBookToCart"
    @decrement-book="decrementBookToCart"
  />
</main>
```

A versão completa do arquivo `App.vue` está no bloco abaixo.

???info ":eye::eye: Versão completa"

    ```vue title="./src/App.vue" linenums="1" hl_lines="8 79"
    <script setup>
    import { ref } from 'vue'

    import FooterComponent from '@/components/FooterComponent.vue'
    import HeroBanner from '@/components/HeroBanner.vue'
    import FeaturedComponent from '@/components/FeaturedComponent.vue'
    import HeaderComponent from '@/components/HeaderComponent.vue'
    import CartComponent from '@/components/CartComponent.vue'

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
        <cart-component
          :cart="cart"
          @hide-cart="showCart = false"
          @increment-book="incrementBookToCart"
          @decrement-book="decrementBookToCart"
        />
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
    </style>
    ```
