# Projeto do novo Carrinho - Frontend

## O que é o projeto


Este projeto tem a finalidade de complementar o projeto do novo carrinho. Ele foi desenvolvido utilizando Angular em sua versão 1.5.3 e jQuery na versão 1.11.3.

Este projeto consome a API existente utilizando funções nativas do AngularJS.


## Instalação do Projeto

Para a instalação do projeto, é necessário ter instalado o gerenciador de pacotes NPM, task runner GRUNT e o pre-processador de CSS SASS.

```shell
sudo apt-get install npm gem
```
```shell
gem install sass
```

```shell
sudo npm install -g grunt-cli
```
Agora basta instalar as dependências listadas no package.json com o seguinte comando.

```shell
npm install
```

## Desenvolvimento

Após a instalação, para minificar e testar os assets basta utilizar o Grunt

```shell
grunt checkout
```

O comando acima executa 4 tarefas

- JSHINT  - Testa os scripts para verificar erro de sintaxe
- JASMINE - Testa algumas funções importantes. O arquivo de teste do jamine está em assets/js/tests/spec
- UGLIFY  - Minifica e unifica arquivos de JavaScript
- CSSMIN  - Minifica e unifica arquivos de CSS

Ambos os testes param a execução das tarefas em caso de erro.

O comando abaixo, executa as tarefas JSHINT,UGLIFY e CSSMIN em cada alteração nos arquivos

- assets/js/oi-functions.js
- assets/css/style.css

```shell
grunt w
```

## Estrutura de arquivos

A raiz do projeto conta com a seguinte estrutura de arquivos:

ROOT
- app
- assets
- views
- node_modules

Dessa estrutura as pastas onde é necessário atenção são

- *ROOT/app/controllers/*

Onde temos os controllers que consomem e tratam os dados da API

- *ROOT/app/http/*

Onde temos o arquivo de rotas, configurações e funções para consumir a API

- *ROOT/app/assets/*

Onde temos todos os assets para a aplicação.
