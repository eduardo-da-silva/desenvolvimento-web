# Informações iniciais

Essas são notas de aula para o uso nas disciplinas de desenvolvimento web dos professores Eduardo da Silva e Kennedy Araújo.

Esse material ainda está em construção e o seu conteúdo é melhor absorvido durante as atividades realizadas em sala de aula.

## Trilha do Curso

Esse curso é parte de uma trilha de aprendizado. Siga os links abaixo para acessar os outros cursos da trilha:

- **[Programação I](https://github.com/ldmfabio/Programacao)** ([Prof. Fábio Longo de Moura](https://github.com/ldmfabio))
  - Lógica de Programação usando JavaScript
- **[Desenvolvimento Web II](https://eduardo-da-silva.github.io/desenvolvimento-web/)** ([Prof. Eduardo da Silva](https://github.com/eduardo-da-silva/) e [Prof. Kennedy Araújo](https://github.com/kennedyaraujo))
  - Desenvolvimento front-end com VueJS
- **[Desenvolvimento Web III](https://github.com/marrcandre/django-drf-tutorial)** ([Prof. Marco André Lopes Mendes](https://github.com/marrcandre))
  - Desenvolvimento back-end com Django e DRF.
- **[Desenvolvimento Dispositivos móveis III](https://eduardo-da-silva.github.io/aula-desenvolvimento-mobile/)** ([Prof. Eduardo da Silva](https://github.com/eduardo-da-silva/))
  - Desenvolvimento para dispositivos móveis com Vue + Vite + PWA.

Bons estudos!

## Configurando o ambiente

### Instalação da versão LTS do NodeJS

Recomendo a utilização do `nvm`, que permite a utilização de versões diferentes do NodeJS. O nvm é gerenciador de versões do NodeJs, desenvolvido para ser instalado utilizando a conta de um usuário final.

Para instalar ou atualizar o o `nvm`, execute o comando abaixo:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```

Após a instalação, é necessário atualizar as variáveis de ambiente do seu terminal. Para tal, sugiro **fechar o terminal e abrir novamente**. Em seguida, você pode instalar a versão LTS do NodeJS:

```bash
nvm install --lts
```

???tip "Para quem utiliza o zsh"

    Caso você esteja utilizando o ambiente `zsh`, é necessário editar o arquivo `~/.zshrc` e adicione as seguintes linhas:

    ```bash
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
    ```

### Configuração das variáveis de ambiente do GIT

Considerando que o `git` já esteja instalado em seu ambiente, sugiro configurar as variáveis de ambiente com as informações do usuário e email para registros nos _commits_ do repositório. Para isso, execute os seguintes comandos:

```bash
git config --global user.name "Nome do usuário"
git config --global user.email "email@dominio.com"
```

!!!note "Ambiente no Microsoft Windows"

    Foi criada uma playlist no [Youtube](https://www.youtube.com/watch?v=R9cgjP5HLzE&list=PL6u1VNwqZdJamJIpi0ajtFpopTWeUx5pK). Existem algumas dicas boas quanto à instalação e permissão de acesso.

    Um comando quase sempre necessário no Windows, para ser executado no Power Shell, é:

    ```bash
    Set-ExecutionPolicy Unrestricted -Scope CurrentUser
    ```

### Extensões recomendadas do Visual Studio Code

Eu sugiro que você instale as seguintes extensões para o Visual Studio Code:

- [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar)
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [Portuguese (Brazil) Language Pack](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-pt-BR)
- [vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons)

Você pode instalar outras extensões e fazer configurações adicionais, conforme a sua preferência.
