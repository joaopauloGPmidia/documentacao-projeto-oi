# Projeto do novo Carrinho - Backend

## O que é o projeto


Este projeto tem a finalidade de complementar o projeto do novo carrinho. Este projeto foi desenvolvido em [PHP][1] na versão 5.5.9 utilizando o framework [Laravel][2] na versão 5.2.


Este projeto contém duas partes importantes: o CMS para complementar dados de produto e adicionar outras funções ao front e também uma API REST para as funções do CMS e auxiliar outras integrações.


## O CMS conta com as seguintes funcionalidades:


- Cupons de Desconto
- Descritivo de Produtos
- Cross Selling
- Visualizador de Carrinhos

### Cupons de Desconto
Essa funcionalidade permite que se cadastre um produto principal sem desconto, e o seu respectivo produto já com o valor de descontado ou com a promoção já inclusa. No momento que o usuário utilizar o cupom cadastrado, o sistema checa se o cupom é válido, e faz a troca de produtos direto no carrinho.

### Descritivo de Produtos
Aqui a equipe do marketing consegue cadastrar uma descrição mais comercial, e adicionar um thumb para o produto, informações que são apresentadas na telas onde o produto é exibido.

### Cross Selling
Após a finalização da compra, no front será exibido sugestões de produtos previamente cadastrados, para cada um dos produtos. Podendo ter até dois níveis de sugestão. Ex:

| Produto Comprado  | Produto Sugerido Nível 1  | Produto Sugerido Nível 2  |
|:---------------:  | :-----------------------: | :-----------------------: |
| Educa+            | Office 360                | Suporte MD                |


### Visualizador de Carrinhos
Aqui a equipe de marketing consegue visualizar os "carrinhos" dos usuários que adicionaram produtos e fizeram login (mesmo se não finalizar o pagamento). Assim é possível realizar campanhas de incentivo para a finalização da compra, ou sugerir novos produtos e etc.

## Estrutura de arquivos

A raiz do projeto conta com a seguinte estrutura de arquivos:

ROOT
- app
- bootstrap
- config
- database
- public
- resources
- storage
- tests
- vendor

Dessa estrutura as pastas onde é necessário atenção são (as demais são de uso do framework e não necessariamente são utilizadas)

- ROOT/app/Http/Controllers/ApiV1

Onde temos os controllers da API

- ROOT/app/Http/Controllers/

Onde temos os controllers do CMS

- ROOT/app/Http/routes.php

Onde definimos todas as rotas da aplicação, tanto do CMS quando da API

- ROOT/config/database.php

Onde é adicionado as configurações do banco de dados, as configurações já estão parametrizadas para utilizar mongodb, e os dados de acesso ao banco de dados estão em um arquivo na raiz chamado .env

- ROOT/resources

Onde temos as views e os arquivos estáticos do CMS

- ROOT/storage

Onde as imagens dos produtos cadastrados no CMS são guardadas

- ROOT/vendor


Onde as bibliotecas utilizadas no projeto são instaladas


- ROOT/.env

Arquivo texto simples onde são guardadas as configurações de banco de dados e urls de acesso, essas informações são guardadas em uma sintaxe simples de CHAVE=VALOR

- ROOT/database-updater.php

Script PHP utilizado para popular um banco de dados local, com informações dos produtos disponibilizados nas seguintes urls:


http://servicos.oi.com.br/api/atualizar-produtos/residencial

http://servicos.oi.com.br/api/atualizar-produtos/empresarial

- ROOT/database-updater.php

Sempre que alguma informação de produto for atualizada, como preço, nome etc, esse script deve ser rodado. E sempre que for realizada uma nova instalação desse projeto, o script também deve ser atualizado.

[1]: https://secure.php.net/
[2]: https://laravel.com/
