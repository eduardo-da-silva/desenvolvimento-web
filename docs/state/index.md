# Gerenciamento de estados

## Conceitos de gerenciamento de estados

O gerenciamento de estados é uma parte importante do desenvolvimento de aplicações web. Ele é responsável por manter o estado da aplicação sincronizado com a interface de usuário, garantindo que as informações exibidas na tela estejam sempre atualizadas.

No Vue.js, o gerenciamento de estados é feito por meio de variáveis reativas, que são propriedades da instância Vue que podem ser monitoradas e reagir a mudanças. Quando uma variável reativa é alterada, o Vue.js automaticamente atualiza a interface de usuário para refletir essa mudança.

No entanto, vamos considerar a aplicação de exemplo que fizemos na aula anterior, para listagem e exclusão de produtos. Nessa aplicação, a listagem de produtos é feita por meio de um componente ProductList, que recebe um array de produtos como propriedade e emite um evento quando o usuário clica em um ícone de lixeira para excluir um produto.

Contudo, considere que o usuário clique no ícone de lixeira para excluir um produto. Nesse caso, o componente ProductList emite um evento para o componente pai, que é responsável por remover o produto da lista. A remoção do produto é refletida na interface de usuário, pois a variável reativa que armazena a lista de produtos é atualizada.

Porém se o usuário clicar para ver os detalhes de um produto e depois retornar para a listagem de produtos, a lista de produtos será recarregada para o estado inicial, ou seja, as alterações ou exclusões de produto são perdidas. Isso ocorre porque a lista de produtos é uma variável local do componente e não é compartilhada com outros componentes.

E esse comportamento pode ser um problema em aplicações maiores, onde vários componentes precisam compartilhar o mesmo estado. Para resolver esse problema, o Vue.js fornece uma solução chamada Pinia, que é uma biblioteca de gerenciamento de estados com uma interface simples e intuitiva.

## Pinia

Pinia é uma biblioteca de gerenciamento de estados para Vue.js que fornece uma maneira simples e intuitiva de compartilhar estados entre componentes.

Com Pinia, é possível criar um store global que armazena o estado da aplicação e compartilhá-lo com todos os componentes que precisam acessar ou modificar esse estado. Dessa forma, é possível manter o estado da aplicação sincronizado entre os diferentes componentes, garantindo que as informações exibidas na tela estejam sempre atualizadas.

Nas próximas aulas, vamos aprender a criar um store global com Pinia e utilizá-lo para gerenciar o estado da aplicação. Vamos ver como definir o estado da aplicação, como acessar e modificar esse estado a partir dos componentes e como reagir a mudanças no estado para atualizar a interface de usuário.

Também, partiremos da aplicação de exemplo que fizemos na aula anterior, quando estudamos os conceitos do vue-router. A aplicação em questão faz a listagem e exclusão de produtos, e vamos refatorá-la para utilizar Pinia. Vamos ver como criar um store global para armazenar a lista de produtos e como compartilhar esse estado entre os diferentes componentes da aplicação.

### Instalação do Pinia

Como no caso do VueRouter, o Pinia é uma biblioteca externa que precisa ser instalada no projeto. Para isso, você pode escolher incluí-la no momento da criação do projeto ou instalá-la posteriormente. Para instalar o Pinia em um projeto existente, você pode usar o seguinte comando:

```bash
npm install pinia
```

Em seguida, você precisa configurar o Pinia no seu projeto Vue.js. Para isso, abra o arquivo `src/main.js` e adicione o seguinte código:

```javascript title="src/main.js"
import { createPinia } from 'pinia';

const pinia = createPinia();
app.use(pinia);
```

A versão completa do arquivo `src/main.js` ficará assim:

???info ":eye::eye: Versão completa"

    ```javascript title="./src/main.js" linenums="1" hl_lines="5 10 13"
    import '@mdi/font/css/materialdesignicons.min.css'
    import './assets/main.css'

    import { createApp } from 'vue'
    import { createPinia } from 'pinia'

    import router from './router'
    import App from './App.vue'

    const pinia = createPinia()

    const app = createApp(App)
    app.use(pinia)
    app.use(router)
    app.mount('#app')
    ```

Com isso, o Pinia estará configurado e pronto para ser utilizado no seu projeto Vue.js. Agora, você pode começar a criar stores e gerenciar o estado da sua aplicação de forma eficiente.

### Criando um store com Pinia

Para criar um store com Pinia, você precisa definir um arquivo que exporta uma função que cria o store. Essa função deve retornar um objeto que contém o estado, as ações e os getters do store.

Vamos criar um store para gerenciar o carrinho e a sua visualização. Crie um arquivo chamado `cart.js` dentro da pasta `src/stores` e adicione o seguinte código:

```javascript title="src/stores/cart.js"
import { ref } from 'vue';
import { defineStore } from 'pinia';

export const useCartStore = defineStore('cart', () => {
  const showCart = ref(false);

  const cart = ref({
    items: [],
    total: 0,
  });

  function decrementBookToCart(book) {
    const existingBook = cart.value.items.find((item) => item.id === book.id);
    if (existingBook.quantity === 1) {
      cart.value.items = cart.value.items.filter((item) => item.id !== book.id);
    } else {
      existingBook.quantity--;
    }
    cart.value.total -= book.price;
  }

  function incrementBookToCart(book) {
    const existingBook = cart.value.items.find((item) => item.id === book.id);
    existingBook.quantity++;
    cart.value.total += book.price;
  }

  function addToCart(book) {
    const existingBook = cart.value.items.find((item) => item.id === book.id);
    if (existingBook) {
      existingBook.quantity++;
    } else {
      cart.value.items.push({ ...book, quantity: 1 });
    }
    cart.value.total += book.price;
    alert(`Adicionado ${book.title} ao carrinho!`);
  }

  return {
    showCart,
    cart,
    incrementBookToCart,
    decrementBookToCart,
    addToCart,
  };
});
```

Nesse caso, estamos criando um store chamado `cart` que contém duas variáveis reativas: `showCart` e `cart`. A função `defineStore` é usada para definir o store e o nome do store é passado como primeiro argumento.

Também, definimos três funções: `incrementBookToCart`, `decrementBookToCart` e `addToCart`. Essas funções são responsáveis por manipular o estado do carrinho, adicionando ou removendo livros e atualizando o total do carrinho. Note que essas funções já estavam desenvolvidas anteriormente, mas agora estão encapsuladas dentro do store.

### Utilizando o store no componente

Agora que temos o store criado, podemos utilizá-lo nos nossos componentes. Para isso, vamos importar o store e usar a função `useCartStore` para acessar o estado do carrinho.

Primeiramente, vamos ajustar o componente `HeaderComponent.vue` para usar o store do carrinho. Abra o arquivo `src/components/HeaderComponent.vue` e modifique o bloco `<script setup>` para incluir o uso do store:

```vue title="src/components/HeaderComponent.vue"
<script setup>
import { useCartStore } from '@/stores/cart';
const cartStore = useCartStore();
</script>
```

Agora, para exibir o carrinho, vamos usar a variável `showCart` do store. No bloco `<template>`, modifique o código para usar `cartStore.showCart`:

```vue title="./src/components/HeaderComponent.vue" linenums="25"
        <li @click="cartStore.showCart = !cartStore.showCart">
```

Note que alteramos o evento de clique para alternar o valor de `showCart` diretamente do store. Isso garante que o estado do carrinho seja compartilhado entre os componentes. Dessa forma, a função de `emit` que antes era usada para emitir o evento `click-cart` não é mais necessária, pois estamos manipulando o estado diretamente do store.

???info ":eye::eye: Versão completa"

    ```vue title="./src/components/HeaderComponent.vue" linenums="1" hl_lines="2-3 25"
    <script setup>
        import { useCartStore } from '@/stores/cart'
        const cartStore = useCartStore()
    </script>

    <template>
        <header>
            <nav>
                <h1>
                    <RouterLink to="/">
                    IFbooks
                    <span class="logo-title"> Apreço a livros </span>
                    </RouterLink>
                </h1>
                <div class="search-wrapper">
                    <input type="text" class="search" placeholder="Buscar..." />
                </div>
                <ul>
                    <li>Termos</li>
                    <li><RouterLink to="/equipe">Equipe</RouterLink></li>
                    <li>Envio</li>
                    <li>Devoluções</li>
                </ul>
                <ul class="icons">
                    <li @click="cartStore.showCart = !cartStore.showCart">
                    <span class="mdi mdi-cart"></span>
                    </li>
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

        & a {
            text-decoration: none;
            color: #000;
        }

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

### Definindo uma store para os livros.

Agora, vamos criar um store para gerenciar os livros. Crie um arquivo chamado `books.js` dentro da pasta `src/stores` e adicione o seguinte código:

```javascript title="./src/stores/books.js" linenums="1"
import { ref } from 'vue';
import { defineStore } from 'pinia';

export const useBooksStore = defineStore('books', () => {
  const books = ref([
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
  ]);

  return { books };
});
```

Note que, como no caso do store do carrinho, estamos usando a função `defineStore` para definir o store dos livros. O estado do store é uma variável reativa chamada `books`, que contém um array de objetos representando os livros disponíveis. Também, essas informações já estavam definidas anteriormente, mas agora estão encapsuladas dentro do store.

### Utilizando o store dos livros no componente HomeView

Agora, vamos editar o arquivo `src/views/HomeView.vue` para utilizar o store do carrinho. Abra o arquivo e deixe o seu conteúdo como abaixo (as novas linhas adicionadas estão destacadas):

```vue title="src/views/HomeView.vue" linenums="1" hl_lines="7-10 15-18 25 26"
<script setup>
import CartComponent from '@/components/CartComponent.vue';
import HeroBanner from '@/components/HeroBanner.vue';
import FeaturedComponent from '@/components/FeaturedComponent.vue';
import BooksListing from '@/components/BooksListing.vue';

import { useBooksStore } from '@/stores/books';
import { useCartStore } from '@/stores/cart';
const booksStore = useBooksStore();
const cartStore = useCartStore();
</script>

<template>
  <cart-component
    v-if="cartStore.showCart"
    :cart="cartStore.cart"
    @hide-cart="cartStore.showCart = false"
    @increment-book="cartStore.incrementBookToCart"
    @decrement-book="cartStore.decrementBookToCart"
  />
  <template v-else>
    <hero-banner />
    <featured-component />
    <books-listing
      :books="booksStore.books"
      @add-to-cart="cartStore.addToCart"
    />
  </template>
</template>
```

Temos, agora, importado os stores `useBooksStore` e `useCartStore`, e instanciado as variáveis `booksStore` e `cartStore`. Essas variáveis nos permitem acessar o estado dos livros e do carrinho, respectivamente. Além disso, o componente `CartComponent` agora recebe o estado do carrinho diretamente do store, e o componente `BooksListing` recebe a lista de livros do store dos livros.
