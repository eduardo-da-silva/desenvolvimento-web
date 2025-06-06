## Instalação e configuração básica

!!!note Observação

    Faremos todos os código na continuação do projeto que já estamos desenvolvendo com o carrinho de compras da livraria. Poderíamos ter feito a criação do projeto já com o Vue-Router

Para instalar o Vue Router em um projeto VueJS, você pode usar o seguinte comando:

```bash
npm install vue-router@4
```

Após a instalação, você pode configurar o Vue Router no seu projeto. Para isso, crie um arquivo chamado `index.js` na pasta `src/router` (1) do seu projeto e adicione o seguinte código:
{ .annotate }

1.  :man_raising_hand: Crie a pasta `src/router` caso ela não exista.

```javascript title="./src/router/index.js" linenums="1"
import { createRouter, createWebHistory } from 'vue-router';

const routes = [];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router;
```

Nesse código, estamos importando as funções `createRouter` e `createWebHistory` do Vue Router. Em seguida, definimos um array `routes` que será usado para armazenar as rotas da nossa aplicação. Por enquanto, deixamos esse array vazio. Depois disso, criamos uma instância do roteador usando a função `createRouter`, passando o histórico de navegação e as rotas definidas. Por fim, exportamos o roteador para que possamos usá-lo em outros arquivos.

Agora, precisamos importar o roteador no arquivo principal da nossa aplicação, que é o arquivo `main.js`. Abra esse arquivo e adicione o seguinte código:

```javascript title="./src/main.js" linenums="1"
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

createApp(App).use(router).mount('#app');
```

Nesse código, estamos importando o roteador que acabamos de criar e usando o método `use` para registrá-lo na instância da aplicação Vue. Isso permite que o Vue Router gerencie as rotas da nossa aplicação.

### Criando a página principal

Agora que configuramos o Vue Router, podemos começar a definir as rotas da nossa aplicação. Inicialmente, vamos criar um componente que será a página principal da nossa aplicação. Crie um arquivo chamado `HomeView.vue` na pasta `src/views` (1) do seu projeto e adicione o seguinte código:
{ .annotate }

1.  :man_raising_hand: Crie a pasta `src/views` caso ela não exista.

```vue title="./src/views/HomeView.vue" linenums="1"
<script setup>
import { ref } from 'vue';
import FeaturedComponent from '@/components/FeaturedComponent.vue';
import HeroBanner from '@/components/HeroBanner.vue';
import CartComponent from '@/components/CartComponent.vue';
import BooksListing from '@/components/BooksListing.vue';

const showCart = ref(false);
const cart = ref({
  items: [],
  total: 0,
});
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
];

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
</script>

<template>
  <CartComponent
    v-if="showCart"
    :cart="cart"
    @hide-cart="showCart = false"
    @increment-book="incrementBookToCart"
    @decrement-book="decrementBookToCart"
  />
  <template v-else>
    <button @click="showCart = true">Ir para carrinho</button>>
    <HeroBanner />
    <FeaturedComponent />
    <BooksListing :books="books" @add-to-cart="addToCart" />
  </template>
</template>
```

Note que praticamente copiamos o código do componente `App.vue` que já havíamos criado anteriormente. A diferença é que agora estamos usando o Vue Router para gerenciar as rotas da nossa aplicação. O componente `HomeView.vue` será a página principal da nossa aplicação e será exibido quando o usuário acessar a rota `/`. Também não precisamos importar o componente `HeaderComponent` e `FooterComponent`, pois eles serão parte do layout da nossa aplicação e ficarão fora do componente `HomeView.vue`.

Ainda, criamos um botão que, quando clicado, exibe o carrinho de compras. O carrinho de compras é um componente separado que será exibido quando o usuário clicar no botão "Ir para carrinho". Note que tivemos que fazer isso pois a funcionalidade de abrir o carrinho a partir do `HeaderComponent` não estará disponível, já que não estamos mais usando o `App.vue` como componente raiz. Isso será resolvido mais adiante, em outros conceitos que vamos adquirir.

### Criando uma página para a equipe

Vamos também criar um componente que terá as informações da equipe de desenvolvimento. Crie um arquivo chamado `TeamView.vue` na pasta `src/views` do seu projeto e adicione o seguinte código:

```vue title="./src/views/TeamView.vue" linenums="1"
<template>
  <div>
    <h1>Equipe de Desenvolvimento</h1>
    <ul>
      <li>Desenvolvedor 1</li>
      <li>Desenvolvedor 2</li>
      <li>Desenvolvedor 3</li>
    </ul>
  </div>
</template>
```

### Configurando as rotas

Agora que temos os componentes `HomeView.vue` e `TeamView.vue`, podemos configurar as rotas da nossa aplicação. Abra o arquivo `src/router/index.js` e adicione as seguintes rotas:

```javascript title="./src/router/index.js" linenums="1"
import { createRouter, createWebHistory } from 'vue-router';
import HomeView from '@/views/HomeView.vue';

const routes = [
  {
    path: '/',
    name: 'Home',
    component: HomeView,
  },
  {
    path: '/equipe',
    name: 'Team',
    component: () => import('@/views/TeamView.vue'),
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router;
```

Note que usamos duas formas de importar os componentes. Para a rota da página inicial, importamos o componente `HomeView` diretamente. Já para a rota da equipe, usamos uma importação assíncrona. Você pode usar essa abordagem para carregar componentes sob demanda, o que pode melhorar o desempenho da sua aplicação, especialmente se você tiver muitos componentes ou páginas.

## Os comandos RouterLink e RouterView

Agora que temos as rotas configuradas, precisamos usar os componentes `<RouterLink />` e `<RouterView />` do Vue Router para navegar entre as páginas da nossa aplicação.

O comando RouterView é usado para renderizar o componente correspondente à rota atual. Ele deve ser usado no componente raiz da sua aplicação, geralmente no arquivo `App.vue`. O Vue Router irá renderizar o componente correspondente à rota atual dentro do `<RouterView />`.

O comando RouterLink é usado para criar links que, quando clicados, navegam para a rota especificada. Ele deve ser usado dentro do componente `<template />` para criar links de navegação entre as páginas da sua aplicação. O Vue Router irá interceptar os cliques nos links criados com `<RouterLink />` e navegar para a rota especificada, sem recarregar a página.

Vamos ajustar o nosso projeto para usar esses componentes.

### Ajustando o arquivo `App.vue`

Agora, precisamos ajustar o arquivo `App.vue` para usar o Vue Router e exibir as rotas corretamente. Abra o arquivo `src/App.vue` e substitua o conteúdo pelo seguinte:

```vue title="./src/App.vue" linenums="1"
<script setup>
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from '@/components/FooterComponent.vue';
</script>

<template>
  <HeaderComponent @click-cart="showCart = !showCart" />
  <main>
    <RouterView />
  </main>
  <footer-component />
</template>

<style scoped></style>
```

Nesse código, estamos importando o componente `HeaderComponent` e `FooterComponent`, e usando o componente `<RouterView />` para renderizar as rotas definidas no Vue Router. O `<RouterView />` é um componente especial do Vue Router que renderiza o componente correspondente à rota atual.

Dessa forma, no local onde está definido o componente `<RouterView>`, o Vue Router irá renderizar o componente correspondente à rota atual. Por exemplo, se o usuário acessar a rota `/`, o componente `HomeView` será exibido. Se o usuário acessar a rota `/equipe`, o componente `TeamView` será exibido.

### Criando um link para a página da equipe e Home

Para navegar entre as páginas da nossa aplicação, podemos usar o componente `<RouterLink />` do Vue Router. Esse componente permite criar links que, quando clicados, navegam para a rota especificada.

Abra o arquivo `src/components/HeaderComponent.vue` e altere o bloco de `template` para o seguinte código:

```vue title="./src/components/HeaderComponent.vue" linenums="5" hl_lines="5-8 15"
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
        <li @click="$emit('click-cart')"><span class="mdi mdi-cart"></span></li>
        <li><span class="mdi mdi-heart"></span></li>
        <li><span class="mdi mdi-account"></span></li>
      </ul>
    </nav>
  </header>
</template>
```

Note as alterações que fizemos nas linhas destacadas (linhas 9 a 12 e linha 19). A versão completa do arquivo `HeaderComponent.vue` está no bloco abaixo.

???info ":eye::eye: Versão completa"

    ```vue title="./src/components/HeaderComponent.vue" linenums="1" hl_lines="5-8 15"
    <script setup>
        defineEmits(['click-cart'])
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

            & a {
                text-decoration: none;
                color: rgb(44, 62, 80);
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

Agora a nossa aplicação está pronta para ser testada.
