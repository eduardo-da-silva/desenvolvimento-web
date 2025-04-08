## Correção dos exercícios

Faremos a correção dos exercícios usando a API de composição. Vamos, além disso, corrigir todos os itens num só exemplo. Contudo, sugiro que você tente resolver os exercícios antes de ver a correção.

??? example "Correção dos exercícios"

    ```html title="./src/App.vue" linenums="1"
    <script setup>
      import { ref } from 'vue';

      const nome = ref('Seu nome');
      const idade = ref(20);
      const contador = ref(0);

      function incrementar() {
        contador.value++;
      }

      function decrementar() {
        if (contador.value > 0) {
          contador.value--;
        }
      }

      function reiniciar() {
        contador.value = 0;
      }

      function inverterTextoEmMaiusculo(texto) {
        return texto.split('').reverse().join('').toUpperCase();
      }
    </script>

    <template>
      <h1>Correção dos exercícios</h1>
      <div class="info">
        <h2>Informações</h2>
        <p>Nome: {% raw %}{{ nome }} {% endraw %}</p>
        <p>Idade: {% raw %}{{ idade }} {% endraw %} anos</p>
        <hr />
        <p>
          Para completar 50 anos faltam: {% raw %}{{ 50 - idade }} {% endraw %} anos
        </p>
        <p>O nome tem {% raw %}{{ nome.length }} {% endraw %} caracteres</p>
        <p>
          O nome invertido em maiúscula é: {% raw %}{{
          inverterTextoEmMaiusculo(nome) }} {% endraw %}
        </p>
      </div>
      <div class="contador">
        <h2>Contador</h2>
        <p>Valor: {% raw %}{{ contador }} {% endraw %}</p>
        <button @click="incrementar">Incrementar</button>
        <button @click="decrementar">Decrementar</button>
        <button @click="reiniciar">Reiniciar</button>
        <div
          :style="{% raw %}{ backgroundColor: contador > 10 ? 'green' : 'red' }{% endraw %}"
        >
          <p v-if="contador > 10">Valor maior que 10</p>
          <p v-else>Valor menor que 10</p>
        </div>
      </div>
    </template>

    <style scoped>
      .info,
      .contador {
        background-color: rgba(35, 12, 22, 1);
        padding: 20px 30px;
        color: rgb(183, 210, 219);
        border-radius: 10px;
      }

      h1 {
        color: darkblue;
        font-weight: bold;
        font-size: 1.5em;
      }

      button {
        margin: 10px;
        padding: 10px;
        border: 0;
        border-radius: 5px;
        background-color: lightblue;
        color: black;
        font-weight: bold;
        cursor: pointer;
      }

      button:hover {
        background-color: blue;
      }

      div {
        margin: 10px 0;
        padding: 10px;
        border-radius: 5px;
        color: white;
        font-weight: bold;
      }
    </style>
    ```

Esta é a correção dos exercícios. Neste exemplo, usamos a API de composição para criar um contador e mostrar informações na tela. Além disso, corrigimos o nome invertido em maiúsculas e adicionamos um quadro com o contador e a `div` que muda de cor e aparece de acordo com o valor do contador.

Note que esta é uma das formas de corrigir os exercícios. Existem outras formas de fazer a mesma coisa. O importante é entender o conceito e a sintaxe de templates do Vue 3.
