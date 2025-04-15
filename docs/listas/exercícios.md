## Exercícios

Para fixar o conteúdo, vamos resolver alguns exercícios.

### Exercício 1

Faça uma tela que renderize uma lista de cidades. O componente deve receber um array de cidades como propriedade. A lista deve ser renderizada em um elemento `ul`. Cada item da lista deve ser renderizado em um elemento `li`. As cidades iniciais devem ser:

```js
[
  'São Paulo',
  'Rio de Janeiro',
  'Belo Horizonte',
  'Salvador',
  'Fortaleza',
  'Curitiba',
  'Manaus',
  'Recife',
  'Porto Alegre',
  'Brasília',
];
```

### Exercício 2

Usando o mesmo Array do exercício anterior, deve ser renderizada uma lista deve ser renderizada em ordem alfabética. A lista deve ser renderizada em um elemento `ul`. Cada item da lista deve ser renderizado em um elemento `li`. _Dica_: para ordenar um array, você pode usar o método `sort` do array, preferencialmente em uma propriedade computada.

### Exercício 3

Neste exercício você deve criar uma lista de notícias (newsletter), contendo `título`, `data`, `resumo da notícia`, `link da notícia` e, opcionalmente, a `imagem da notícia`. Deve haver um botão que, quando clicado, direcionará para a página da notícia, abrindo o link em uma nova aba. Note que você deve abrir a url que está informada na chave `link` do objeto.

_Dica 1_: como o link está numa variável e você precisa atribuir esse valor para o atributo `href` da tag `a`, você pode usar a diretiva v-bind para fazer isso.

_Dica 2_: para as imagens você pode apenas usar o endereço público da Internet de uma imagem.

Abaixo, um exemplo de como o objeto de notícias pode ser estruturado:

```js
noticias = [
  {
    titulo: 'Título 1',
    data: '01/01/2023',
    resumo: 'Resumo da notícia 1',
    link: 'https://www.google.com',
    imagem: 'https://placehold.co/600x400.png',
  },
  {
    titulo: 'Título 2',
    data: '02/01/2023',
    resumo: 'Resumo da notícia 2',
    link: 'https://www.google.com',
    imagem: 'https://placehold.co/600x400.png',
  },
];
```
