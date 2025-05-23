## Correção dos exercícios

Faremos a correção dos exercícios usando a API de composição. Vamos, além disso, corrigir todos os itens num só exemplo. Sugiro que você tente resolver os exercícios antes de ver a correção.

??? example "Correção dos exercícios"

    ```html title="./src/App.vue" linenums="1"
    <script setup>
      import { computed, ref } from 'vue';

      const contador1 = ref(0);
      const contador2 = ref(0);
      const valorBooleano = ref(true);

      function incrementar(contador) {
        eval(contador).value++;
      }

      function decrementar(contador) {
        if (eval(contador).value > 0) {
          eval(contador).value--;
        }
      }

      const soma = computed(() => contador1.value + contador2.value);
      const somaPar = computed(() => soma.value % 2 === 0);
      const somaMaiorQue10 = computed(() => soma.value > 10);
    </script>

    <template>
      <h1>Correção dos exercícios</h1>
      <div class="booleano">
        <button @click="valorBooleano = !valorBooleano">
           {{ valorBooleano ? 'Esconder Resultado' : 'Mostrar Resultado' }}

        </button>
      </div>
      <div v-if="valorBooleano">
        <div class="contador">
          <h2>Contador 1</h2>
          <button @click="incrementar('contador1')">Incrementar</button>
          <button @click="decrementar('contador1')">Decrementar</button>
          <p>Valor: {{ contador1 }}</p>
        </div>
        <div class="contador">
          <h2>Contador 2</h2>
          <button @click="incrementar('contador2')">Incrementar</button>
          <button @click="decrementar('contador2')">Decrementar</button>
          <p>Valor: {{ contador2 }}</p>
        </div>
        <div class="soma">
          <h2>Soma</h2>
          <p>Valor:  {{ soma }} </p>
          <div v-if="somaMaiorQue10">
            <p>A soma é maior que 10</p>
          </div>
          <div v-else>
            <p>A soma é menor que 10</p>
          </div>
          <div v-if="somaPar">
            <p>A soma é par</p>
          </div>
          <div v-else>
            <p>A soma é ímpar</p>
          </div>
        </div>
      </div>
    </template>
    ```

Note que esta é uma das formas de corrigir os exercícios. Existem outras formas de fazer a mesma coisa. O importante é entender o conceito e a sintaxe de templates do Vue 3.
