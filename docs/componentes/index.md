# Componentes

## Conceitos

Os componentes são instâncias reutilizáveis de VueJS que podem ser criadas e utilizadas em qualquer parte da aplicação. Eles são compostos por um template, que define a estrutura do componente, e por uma instância Vue, que define o comportamento do componente. Os componentes são uma das principais características do VueJS e são muito úteis para organizar e reutilizar o código de uma aplicação. Ainda, com o uso de componentes, é possível dividir a interface de usuário em partes menores e independentes, o que facilita a manutenção e a evolução da aplicação.

No VueJS, em geral, usamos o conceito de SFC (Single File Component) para criar componentes. Um SFC é um arquivo que contém o template, a lógica e o estilo de um componente em um único lugar, como já temos visto em aulas anteriores.

Durante esta aula, vamos estruturar o projeto da livraria com o uso de componentes, criando componentes para as diversas partes da aplicação, como o cabeçalho, o rodapé e a lista de livros.

Alguns conceitos de reutilização de componentes farão mais sentido quando estudarmos o conceitos de rotas, com o Vue Router. Isso porque a reutilização de componentes é muito útil quando se trabalha com rotas dinâmicas e a criação de páginas com elementos comuns.

--8<-- "docs/componentes/criando-componentes-simples.md"
--8<-- "docs/componentes/replicando-criacao-componentes-simples.md"
--8<-- "docs/componentes/manipulando-eventos.md"
--8<-- "docs/componentes/propriedades.md"
