## Mostrando o carrinho

Agora vamos para uma parte que requer um pouco mais de atenção. Vamos implementar a seção do carrinho, que é uma parte importante da aplicação. Nós não queremos que o carrinho seja exibido o tempo todo, mas sim quando o usuário clicar no ícone do carrinho. Para isso, vamos usar um estado reativo para controlar a exibição do carrinho.

Primeiramente, vamos editar a seção `<script>` do arquivo `src/App.vue` para criar a variável reativa que vai controlar a exibição do carrinho, e também uma variável que vai armazenar os livros que estão no carrinho. Para isso, adicione o seguinte código no bloco `<script>`:

```javascript title="./src/App.vue" linenums="2"
import { ref } from 'vue';
const showCart = ref(false);
const cart = ref({
  items: [],
  total: 0,
});
```

Note que o código acima cria duas variáveis reativas: `showCart` e `cart`. A variável `showCart` é um booleano que controla a exibição do carrinho, enquanto a variável `cart` é um objeto que armazena os itens do carrinho e o total da compra. Depois faremos a lógica para adicionar os livros ao carrinho e calcular o total da compra.

Agora, vamos adicionar a lógica para abrir e fechar o carrinho. Para isso, e altere o seguinte código no bloco `<template>`:

```html title="./src/App.vue" linenums="87" hl_lines="88"
<ul class="icons">
  <li @click="showCart = !showCart"><span class="mdi mdi-cart"></span></li>
  <li><span class="mdi mdi-heart"></span></li>
  <li><span class="mdi mdi-account"></span></li>
</ul>
```

Note que adicionamos um evento `@click` no ícone do carrinho, que altera o valor da variável `showCart`. Quando o usuário clicar no ícone do carrinho, a variável `showCart` será alterada para `true`, e o carrinho será exibido. Quando o usuário clicar novamente no ícone do carrinho, a variável `showCart` será alterada para `false`, e o carrinho será ocultado.

Agora, vamos adicionar o código do carrinho. Para isso, adicione o seguinte código no bloco `<template>`, substituindo a abertura da tag `<main>`, logo após o fechamento da tag `<header>`:

```vue title="./src/App.vue" linenums="94"
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
          <td class="cart-item-subtotal">
            R$ {{ book.price * book.quantity }}
          </td>
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
          <span>Produtos</span> <span>R$ {{ cart.total.toFixed(2) }}</span>
          <span>Frete</span> <span> Grátis</span> <span>Total</span>
          <span>R$ {{ cart.total.toFixed(2) }}</span>
        </div>
        <button>Ir para pagamento</button>
      </div>
    </div>
  </section>
</main>
<main v-else>
```

Note que já na abertura da tag `<main>` (linha 93) foi adicionada uma diretiva `v-if` que verifica se a variável `showCart` é verdadeira. Se for, o carrinho será exibido. Caso contrário, o carrinho não será exibido, e será exibida a _tag_ `<main>` que já existia antes (linhas 149 em diante). Isso garante que o carrinho só será exibido quando o usuário clicar no ícone do carrinho.

Dentro a nova tag `<main>`, foi adicionado o código do carrinho. O carrinho é exibido como uma tabela, onde cada linha representa um livro no carrinho. A tabela possui três colunas: título, quantidade e subtotal. A coluna de título exibe a imagem do livro, o título, o autor e o preço. A coluna de quantidade exibe a quantidade do livro no carrinho e dois botões para aumentar ou diminuir a quantidade. A coluna de subtotal exibe o subtotal do livro (preço \* quantidade). No final da tabela, há um botão para voltar para a loja e um resumo da compra com o total.

O botão adicionado para voltar para a loja tem um evento `@click` que altera o valor da variável `showCart` para `false`, ocultando o carrinho. O resumo da compra exibe o total da compra, que ainda não foi implementado, mas será feito na próxima seção. Por fim, alguns elementos como a aplicação do cupom e o botão para ir para o pagamento foram adicionados, mas ainda não possuem funcionalidade.

Agora, vamos adicionar o CSS para estilizar o carrinho. Para isso, adicione o seguinte código no bloco `<style>` do arquivo `src/App.vue`:

```css title="./src/App.vue" linenums="417"
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
```

Nesse caso, a estilização do carrinho é feita de forma semelhante à estilização das demais seções do projeto, sendo que a tabela do carrinho é estilizada para ter um layout mais limpo e organizado.

O quadro abaixo contém o código completo do que fizemos até agora, atentando-se às partes destacadas, que correspondem ao que foi adicionado ou alterado.

???info ":eye::eye: Versão completa"

    ```vue title="./src/App.vue" linenums="1" hl_lines="2-7 88 94-147 417-539"
    <script setup>
    import { ref } from 'vue'
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
            <li @click="showCart = !showCart"><span class="mdi mdi-cart"></span></li>
            <li><span class="mdi mdi-heart"></span></li>
            <li><span class="mdi mdi-account"></span></li>
          </ul>
        </nav>
      </header>
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
      <footer>
        <nav>
          <section class="upper-footer">
            <div>
              <p class="footer-title">
                <a href="#"> IFbooks </a>
              </p>
              <ul>
                <li><span class="mdi mdi-facebook" /></li>
                <li><span class="mdi mdi-instagram" /></li>
                <li><span class="mdi mdi-twitter" /></li>
              </ul>
            </div>
            <div>
              <p class="contact-text">Contato</p>
              <p><span class="mdi mdi-phone" /> +55 47 99999-9999</p>
              <p><span class="mdi mdi-clock" /> 8h às 23h - Seg a Sex</p>
              <p><span class="mdi mdi-email" /> contato@ifbooks.com.br</p>
              <div class="payment-methods">
                <span class="mdi mdi-visa" />
              </div>
            </div>
          </section>
          <section class="lower-footer">
            <p>&copy; Alguns direitos reservados. IFBooks. 2025</p>
          </section>
        </nav>
      </footer>
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

    footer {
      background-color: #27ae60;
      padding: 2vh 8vw;
      color: #fff;

      .upper-footer {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-bottom: 100px;
        border-bottom: 2px solid #fff;

        & div {
          display: flex;
          flex-direction: column;
          gap: 10px;

          & .footer-title {
            font-size: 1.2rem;
            font-weight: 700;

            & a {
              text-decoration: none;
              color: #fff;
            }
          }

          & .contact-text {
            font-size: 1.1rem;
            font-weight: 700;
          }
        }
      }

      .lower-footer {
        display: flex;
        justify-content: center;
        padding-top: 20px;
        font-size: 0.8rem;
      }

      ul {
        display: flex;
        padding: 0;
        gap: 20px;

        li {
          list-style: none;
          font-size: 1.2rem;
          color: #fff;
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
