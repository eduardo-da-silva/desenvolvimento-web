## Rotas dinâmicas

Agora, vamos aprender como criar rotas dinâmicas no Vue Router. As rotas dinâmicas são úteis quando precisamos exibir conteúdo baseado em parâmetros que podem variar, como IDs de usuários, nomes de produtos, etc.

### Definindo rotas dinâmicas

Para definir uma rota dinâmica, usamos dois pontos (`:`) antes do nome do parâmetro na definição da rota. Para exemplificar, no exemplo da nossa livraria, vamos fazer uma rota que exibe detalhes de um livro específico. A rota pode ser definida da seguinte forma, inserindo mais uma rota na variável `routes`, no arquivo `src/router/index.js`:

!!!danger "Cuidado"

    Note que nos exemplos, em geral, estamos sempre alterando alguma variável já existente. Cuide para não sobrescrever variáveis importantes e nem redefinir variáveis que já existem nos exemplos anteriores.

```javascript title="src/router/index.js" linenums="16"
  {
    path: '/livro/:id',
    name: 'Book',
    component: () => import('@/views/BookView.vue'),
    props: true,
  },
];
```

Nossa versão completa do arquivo `src/router/index.js` ficaria assim:

???info ":eye::eye: Versão completa"

    ```javascript title="src/router/index.js" linenums="1" hl_lines="16-21"
    import { createRouter, createWebHistory } from 'vue-router'

    import HomeView from '@/views/HomeView.vue'

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
        {
            path: '/livro/:id',
            name: 'Book',
            component: () => import('@/views/BookView.vue'),
            props: true,
        },
    ]

    const router = createRouter({
    history: createWebHistory(import.meta.env.BASE_URL),
    routes,
    })

    export default router
    ```

Note que a rota `/livro/:id` define um parâmetro dinâmico chamado `id`. Isso significa que quando o usuário acessar uma URL como `/livro/123`, o Vue Router irá capturar o valor `123` e passá-lo para o componente associado à rota. Também, definimos a propriedade `props: true`, que permite que o parâmetro seja passado como uma propriedade para o componente. Por fim, o componente associado à rota é o `BookView.vue`, que será responsável por exibir os detalhes do livro.

### Criando o componente para a rota dinâmica

Agora, precisamos criar o componente `BookView.vue` que irá exibir os detalhes do livro. Crie um novo arquivo chamado `BookView.vue` na pasta `src/views/`. O conteúdo do arquivo pode ser algo como:

```vue title="src/views/BookView.vue"
<script setup>
defineProps(['id']);
</script>

<template>
  <h1>Detalhes do livro: {{ id }}</h1>
</template>
```

Note que estamos usando a diretiva `defineProps` para receber o parâmetro `id` passado pela rota. No template, exibimos o ID do livro. Este é um exemplo simples, mas você pode expandir esse componente para buscar informações de um livro específico em uma API ou em um banco de dados, por exemplo.

Agora, se você quiser testar a rota dinâmica, você pode acessar a URL `/livro/123` (ou qualquer outro ID) e verá o componente `BookView.vue` renderizando o ID do livro.

No sequência, vamos integrar isso com a listagem de livros que criamos anteriormente, para que possamos clicar em um livro e ser redirecionado para a página de detalhes desse livro.
