## Fixando propriedades e eventos

Já usamos o conceito de propriedades (props) e eventos (emits) em aulas anteriores, e também já o usamos em conjunto. Vamos agora, fazer a criação de mais um componente que precise de props e emits, para fixar o conceito.

No caso anterior, enviamos via _props_ um objeto com os dados do carrinho de compras. Agora, vamos criar um componente que recebe um _array_ de objetos, com as informações dos livros, e exibe esses livros em uma lista. O componente também deve emitir um evento quando o usuário clicar no botão de adicionar ao carrinho. O evento deve enviar o objeto do livro que foi adicionado ao carrinho.

### Componente de Listagem de Livros

Vamos criar um componente chamado `BooksListing.vue` que será responsável por exibir a lista de livros. Esse componente deve receber um _array_ de objetos com as informações dos livros e exibir esses livros em uma lista. O componente também deve emitir um evento quando o usuário clicar no botão de adicionar ao carrinho.

Inicialmente, o componente deve ser criado na pasta `src/components`, com o seguinte conteúdo:

```vue title="./src/components/BooksListing.vue" linenums="1" hl_lines="2-3 8 16"
<script setup>
defineEmits(['add-to-cart']);
defineProps(['books']);
</script>

<template>
  <section class="books">
    <article class="book" v-for="book in books" :key="book.id">
      <img :src="book.cover" :alt="book.title" />
      <h2>{{ book.title }}</h2>
      <p class="book-author">{{ book.author }}</p>
      <span class="price-and-like">
        <p class="book-price">R$ {{ book.price.toFixed(2) }}</p>
        <span class="mdi mdi-heart-outline"></span>
      </span>
      <button @click="$emit('add-to-cart', book)">
        <span class="mdi mdi-cart"></span>Comprar
      </button>
    </article>
  </section>
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

Note que já declaramos as _props_ e os _emits_ do componente. As _props_ são `books`, que é um _array_ de objetos com as informações dos livros, e o evento `add-to-cart`, que é emitido quando o usuário clica no botão de adicionar ao carrinho. O evento deve enviar o objeto do livro que foi adicionado ao carrinho (linha 16).

Vamos agora alterar o arquivo `src/App.vue` para usar o novo componente. Para isso, abra o arquivo `src/App.vue` e adicione o seguinte conteúdo no bloco de script:

```vue title="./src/App.vue" linenums="1" hl_lines="9"
<script setup>
import { ref } from 'vue'

import FooterComponent from '@/components/FooterComponent.vue'
import HeroBanner from '@/components/HeroBanner.vue'
import FeaturedComponent from '@/components/FeaturedComponent.vue'
import HeaderComponent from '@/components/HeaderComponent.vue'
import CartComponent from '@/components/CartComponent.vue'
import BooksListing from '@/components/BooksListing.vue'
...
</script>
```

Também, vamos adicionar o componente `BooksListing` no template do arquivo `src/App.vue`, e passar as _props_ e os _emits_ para o componente. O arquivo deve ficar assim:

```vue title="./src/App.vue" linenums="87" hl_lines="4"
<main v-else>
  <hero-banner />
  <featured-component />
  <books-listing :books="books" @add-to-cart="addToCart" />
</main>
```

A versão completa do arquivo `App.vue` está no bloco abaixo.

???info ":eye::eye: Versão completa"

    ```vue title="./src/App.vue" linenums="1" hl_lines="9 90"
    <script setup>
    import { ref } from 'vue'

    import FooterComponent from '@/components/FooterComponent.vue'
    import HeroBanner from '@/components/HeroBanner.vue'
    import FeaturedComponent from '@/components/FeaturedComponent.vue'
    import HeaderComponent from '@/components/HeaderComponent.vue'
    import CartComponent from '@/components/CartComponent.vue'
    import BooksListing from '@/components/BooksListing.vue'

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
        <books-listing :books="books" @add-to-cart="addToCart" />
      </main>
      <footer-component />
    </template>

    <style scoped>
    </style>
    ```
