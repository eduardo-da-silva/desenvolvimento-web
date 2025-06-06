## Rotas programáticas

Até então, vimos como navegar entre as rotas utilizando o componente `<RouterLink />`. No entanto, em alguns casos, pode ser necessário realizar a navegação de forma programática, ou seja, sem a interação direta do usuário. Isso pode ser útil em situações como:

- Redirecionamento após uma ação do usuário (por exemplo, após o envio de um formulário).
- Navegação com base em uma lógica de negócio (por exemplo, após a autenticação do usuário).
- Navegação com base em eventos externos (por exemplo, após a conclusão de uma requisição assíncrona).

Dessa forma, além de usar os componentes `<RouterLink />` e `<RouterView />`, também podemos navegar entre as rotas programaticamente usando a instância do roteador. Para isso, podemos usar o método `router.push()` para navegar para uma nova rota.

Vamos ver como realizar a navegação programática entre rotas no Vue Router.

### Ajustando o componente de listagem de livros

Para demonstrar a navegação programática, vamos ajustar o componente de listagem de livros que criamos anteriormente. Vamos adicionar um evento de clique em cada livro que redireciona o usuário para a página de detalhes do livro selecionado.
Vamos modificar o componente `BookListing.vue` para incluir a navegação programática.

Primeiro, vamos inserir uma função para fazer a rota programática. No arquivo `src/components/BookListing.vue`, adicione o seguinte código, no bloco `<script setup>`:

```javascript title="./src/components/BookListing.vue" linenums="4"
import { useRouter } from 'vue-router';
const router = useRouter();

function openBook(id) {
  router.push({ name: 'Book', params: { id } });
}
```

Agora, no bloco `<template>`, vamos adicionar um evento de clique no elemento que representa cada livro. No exemplo, farei isso na tag `<img>`, mas poderíamos fazer em qualquer outro local ou elemento. Modifique o código para incluir o evento `@click` que chama a função `openBook`:

```vue title="src/components/BookListing.vue" linenums="15"
<img :src="book.cover" :alt="book.title" @click="openBook(book.id)" />
```

Para confirmar, a versão completa do arquivo `src/components/BookListing.vue` ficará assim:

???info ":eye::eye: Versão completa"

    ```vue title="./src/components/BookListing.vue" linenums="1" hl_lines="4-9 15"
    <script setup>
        defineEmits(['add-to-cart'])
        defineProps(['books'])
        import { useRouter } from 'vue-router'
        const router = useRouter()

        function openBook(id) {
            router.push({ name: 'Book', params: { id } })
        }
    </script>

    <template>
        <section class="books">
            <article class="book" v-for="book in books" :key="book.id">
                <img :src="book.cover" :alt="book.title" @click="openBook(book.id)" />
                <h2>{{ book.title }}</h2>
                <p class="book-author">{{ book.author }}</p>
                <span class="price-and-like">
                    <p class="book-price">R$ {{ book.price.toFixed(2) }}</p>
                    <span class="mdi mdi-heart-outline"></span>
                </span>
                <button @click="$emit('add-to-cart', book)"><span class="mdi mdi-cart"></span>Comprar</button>
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

Agora, quando o usuário clicar em um livro, ele será redirecionado para a página de detalhes do livro correspondente, utilizando a navegação programática.
