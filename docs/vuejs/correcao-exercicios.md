## Correção dos exercícios

Abaixo apresento uma proposta de correção dos exercícios. A correção é apresentada em dois exemplos: um usando a API de opções e outro usando a API de composição. Sugiro que você tente resolver os exercícios antes de ver a correção.

??? example "Correção dos exercícios"

    Abaixo as correções dos exercícios

    === "Correção usando a API de opções"

          ```html title="./src/App.vue" linenums="1"
          <script>
            export default {
              data() {
                return {
                  contador: 0,
                };
              },
              methods: {
                incrementar() {
                  this.contador++;
                },
                decrementar() {
                  if (this.contador > 0) {
                    this.contador--;
                  }
                },
                reiniciar() {
                  this.contador = 0;
                },
              },
            };
          </script>

          <template>
            <div>
              <h1>Contador</h1>
              <p> {{ contador }} </p>
              <button @click="incrementar">Incrementar</button>
              <button @click="decrementar">Decrementar</button>
              <button @click="reiniciar">Reiniciar</button>
            </div>
          </template>
          ```

    === "Correção usando a API de composição"

          ```html title="./src/App.vue" linenums="1"
          <script setup>
            import { ref } from 'vue';

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
          </script>

          <template>
            <div>
              <h1>Contador</h1>
              <p> {{ contador }} </p>
              <button @click="incrementar">Incrementar</button>
              <button @click="decrementar">Decrementar</button>
              <button @click="reiniciar">Reiniciar</button>
            </div>
          </template>
          ```
