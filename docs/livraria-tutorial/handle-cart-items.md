## Adicionando e removendo itens

Vamos agora para a parte final desse tutorial, onde vamos adicionar a funcionalidade de adicionar e remover itens do carrinho. Ainda vamos fazer tudo isso de forma simples, sem usar componentes ou gerenciamento de estados.

Primeiramente, vamos adicionar as funções para adicionar ou remover itens no carrinho. Nós faremos três funções distintas:

- `addToCart`: adiciona um livro ao carrinho.
- `incrementBookToCart`: incrementa a quantidade de um livro já adicionado ao carrinho.
- `decrementBookToCart`: decrementa a quantidade de um livro já adicionado ao carrinho.

As funções devem ser implementadas no arquivo `src/App.vue`, dentro do bloco `<script setup>`. O código deve ficar assim:

```javascript title="./src/App.vue" linenums="66"
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
```

Note que em todos os casos foi recalculado o total do carrinho, que é a soma dos preços de todos os livros. Também, foi adicionado um alerta para informar ao usuário que o livro foi adicionado ao carrinho.

Com as funções já desenvolvidas, vamos agora adicionar os eventos de clique nos botões de adicionar item ao carrinho e também de incrementar e decrementar a quantidade de livros no carrinho. Para isso, vamos editar o arquivo `src/App.vue` e adicionar os eventos de clique nos botões. Serão feitas duas alterações no código. Na primeira, vamos usar as funções `incrementBookToCart` e `decrementBookToCart` para incrementar e decrementar a quantidade de livros no carrinho. Para isso, vamos editar o arquivo `src/App.vue`, e alterar `<div>` que possui a classe `cart-item-quantity` para o seguinte código:

```html title="./src/App.vue" linenums="142"
<div class="cart-item-quantity">
  <button @click="decrementBookToCart(book)" class="plain">
    <span class="mdi mdi-minus" />
  </button>
  {{ book.quantity }}
  <button @click="incrementBookToCart(book)" class="plain">
    <span class="mdi mdi-plus" />
  </button>
</div>
```

Note que foram adicionados os eventos de clique nos botões de incrementar e decrementar a quantidade de livros no carrinho.

Também, vamos adicionar o evento de clique no botão de adicionar livro ao carrinho. Para isso, vamos editar o arquivo `src/App.vue`, e alterar o botão de adicionar livro ao carrinho, dentro do laço de repetição da _tag_ `<article>`, para o seguinte código:

```html title="./src/App.vue" linenums="215"
<button @click="addToCart(book)">
  <span class="mdi mdi-cart"></span>Comprar
</button>
```

Com essas alterações realizadas, o código do arquivo `src/App.vue` deve ficar com o apresentado no quadro abaixo.

???info ":eye::eye: Versão completa"

    ```vue title="./src/App.vue" linenums="1" hl_lines="67-92 142-150 215"
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

    function decrementBookToCart(book) {
      const existingBook = cart.value.items.find((item) => item.id === book.id)
      if (existingBook.quantity === 1) {
        cart.value.items = cart.value.items.filter((item) => item.id !== book.id)
      } else {
        existingBook.quantity--
      }
      cart.value.total -= book.price
    }

    function incrementBookToCart(book) {
      const existingBook = cart.value.items.find((item) => item.id === book.id)
      existingBook.quantity++
      cart.value.total += book.price
    }

    function addToCart(book) {
      const existingBook = cart.value.items.find((item) => item.id === book.id)
      if (existingBook) {
        existingBook.quantity++
      } else {
        cart.value.items.push({ ...book, quantity: 1 })
      }
      cart.value.total += book.price
      alert(`Adicionado ${book.title} ao carrinho!`)
    }
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
                    <button @click="decrementBookToCart(book)" class="plain">
                      <span class="mdi mdi-minus" />
                    </button>
                    {{ book.quantity }}
                    <button @click="incrementBookToCart(book)" class="plain">
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
            <button @click="addToCart(book)"><span class="mdi mdi-cart"></span>Comprar</button>
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
