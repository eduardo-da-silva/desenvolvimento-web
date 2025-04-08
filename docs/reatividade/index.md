# Reatividade

Uma das características mais importantes do VueJS é a reatividade, que define que quando o estado de um objeto é alterado, os objetos que dependem desse estado são atualizados automaticamente. No VueJS, a reatividade é implementada através de um sistema de observação de dados. Assim, quando um dado é alterado, o VueJS atualiza automaticamente a interface do usuário.

De forma bem simplificada, podemos considerar que a reatividade é a forma de criar variáveis no VueJs. É fato que uma variável no VueJS pode ser criada usando os usuais comando `let` ou `const`, mas isso não é o suficiente para que o VueJS entenda que aquela variável é reativa. Para que o VueJS entenda que uma variável é reativa, é necessário que ela seja declarada usando a função `reactive` ou`ref`, que são conhecidas como funções reativas.

Recapitulando, podemos dizer que a reatividade, no VueJS, é a forma de criar variáveis que, quando alteradas, o seu valor é atualizado automaticamente na interface do usuário, e vice-versa.

Outro conceito importante é o de propriedades computadas, que são funções que são executadas automaticamente quando uma variável reativa é alterada. Essas funções também serão apresentadas nesta aula.

--8<-- "docs/reatividade/variaveis-reativas.md"
--8<-- "docs/reatividade/propriedades-computadas.md"
--8<-- "docs/reatividade/exercicios.md"
--8<-- "docs/reatividade/correcao-exercicios.md"
