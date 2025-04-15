## Projeto

Neste projeto você deve desenvolver um protótipo de um carrinho de compras de uma livraria. Nesse caso, crie uma lista fixa de produtos, como descrito abaixo:

!!!example "Estrutura do objeto de produtos"

    ```js title="App.vue"
    const produtos = [
        {
            id: 1,
            titulo: 'Livro 1',
            resenha: 'Descrição breve 1'
            preco: 49.9,
            capa: 'https://placehold.co/600x400.png',
        },
        {
            id: 2,
            titulo: 'Livro 2',
            resenha: 'Descrição breve 2'
            preco: 99.9,
            capa: 'https://placehold.co/600x400.png',
        },
        {
            id: 3,
            titulo: 'Livro 3',
            resenha: 'Descrição breve 3'
            preco: 9.9,
            capa: 'https://placehold.co/600x400.png',
        },
        {
            id: 4,
            titulo: 'Livro 4',
            resenha: 'Descrição breve 4'
            preco: 199.9,
            capa: 'https://placehold.co/600x400.png',
        },
        {
            id: 5,
            titulo: 'Livro 5',
            resenha: 'Descrição breve 5'
            preco: 29.9,
            capa: 'https://placehold.co/600x400.png',
        }
    ];
    ```

O usuário deve poder adicionar os livros ao carrinho. Para isso, deve ser renderizada uma lista de livros. O usuário deve poder clicar em um produto para adicioná-lo ao carrinho. O carrinho deve ser renderizado em uma `div` ou `section` abaixo da listagem dos produtos ou ficar escondida e ser apresentada quando clicar no ícone `carrinho` do `layout` proposto. (_Dica:_ pode ser criada uma variável`booleana` para controlar essa função de visibilidade do carrinho).

Em cada item do carrinho deve ter a opção de adicionar quantidade ou remover o item do carrinho. Ao final, deve ser apresentado o valor total dos itens no carrinho, que pode ser calculado a partir da quantidade de cada item e do preço do livro.

Uma sugestão para a estrutura do objeto do carrinho é:

!!!example "Estrutura do objeto do carrinho"

    ```js title="App.vue"
    const carrinho = {
        items: [
            {
                id: 1,
                nome: 'Livro 1',
                preco: 49.9,
                quantidade: 1,
                valorTotal: 49.9,
                },
            {
                id: 2,
                nome: 'Livro 2',
                preco: 99.9,
                quantidade: 2,
                valorTotal: 199.8,
            },
        ],
        frete: 0,
        desconto: 0,
        total: 288.3,
    };
    ```

Note que o objeto do carrinho possui um atributo `total` que é o valor total dos itens no carrinho. Ainda, note que cada item do carrinho possui um atributo `valorTotal` que é o valor total do item multiplicado pela quantidade (1). Ainda, esses dois valores não devem ser informados pelo usuário, mas sim calculados a partir dos valores informados.
{ .annotate }

1. Esse valor pode também ser calculado direto na renderização do item. Exemplo: {{ item.preco * item.quantidade }}. Mas, nesse caso, o valor total do item não estará disponível para ser usado em outros lugares do código, como no cálculo do total do carrinho.

**Dica 1:** você pode calcular o valor total de cada item da compra ao aumentar ou diminuir a quantidade de itens no carrinho, na mesma função que manipula o incrementar e decrementar item do carrinho.

**Dica 2:** o mesmo pode ser feito com o total da compra, que pode ser recalculado sempre que um item é modificado no carrinho.

**Dica 3:** se você desejar, todos esses cálculos podem ser feitos em propriedades computadas, mas não é obrigatório.

**Dica 4:** um modelo de layout pode ser visto [aqui](https://www.figma.com/design/iY248n1M3QOKwrtlWrZe9K/Untitled?node-id=1-1096&t=69vLGugLA87aupkY-1)
