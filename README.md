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

## Instalação do Projeto

Para a instalação do projeto, é necessário que o servidor esteja preparado com o PHP na versão indicada no inicio do documento, e é necessário também utilizar um servidor HTTP, [Apache][3] ou [Nginx][4] por exemplo.

Na configuração do Virtual Host do servidor HTTP, aponte o Diretório Raiz para RAIZ_DO_PROJETO/public.

Também é necessário que o servidor tenha o [Composer][5] instalado, para que seja possível instalar as dependências do projeto.

Os passos para instalar as dependências são:

- Para uma instalação nova do projeto

```shell
cd RAIZ_DO_PROJETO && composer install --no-scripts
```

- Para uma atualização do projeto

```shell
cd RAIZ_DO_PROJETO && composer update --no-scripts
```

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

- *ROOT/app/Http/Controllers/ApiV1*

Onde temos os controllers da API

- *ROOT/app/Http/Controllers/*

Onde temos os controllers do CMS

- *ROOT/app/Http/routes.php*

Onde definimos todas as rotas da aplicação, tanto do CMS quando da API

- *ROOT/config/database.php*

Onde é adicionado as configurações do banco de dados, as configurações já estão parametrizadas para utilizar mongodb, e os dados de acesso ao banco de dados estão em um arquivo na raiz chamado .env

- *ROOT/resources*

Onde temos as views e os arquivos estáticos do CMS

- *ROOT/storage*

Onde as imagens dos produtos cadastrados no CMS são guardadas

- *ROOT/vendor*


Onde as bibliotecas utilizadas no projeto são instaladas


- *ROOT/.env*

Arquivo texto simples onde são guardadas as configurações de banco de dados e urls de acesso, essas informações são guardadas em uma sintaxe simples de CHAVE=VALOR

- *ROOT/database-updater.php*

Script PHP utilizado para popular um banco de dados local, com informações dos produtos disponibilizados nas seguintes urls:


http://servicos.oi.com.br/api/atualizar-produtos/residencial

http://servicos.oi.com.br/api/atualizar-produtos/empresarial

- *ROOT/database-updater.php*

Sempre que alguma informação de produto for atualizada, como preço, nome etc, esse script deve ser rodado. E sempre que for realizada uma nova instalação desse projeto, o script também deve ser atualizado.

### Sobre os Controllers e Models

Todos os controllers da parte do CMS, seguem o padrão de um controller de CRUD. Ambos tem os metodos de listar todos ou apenas um registro, criar, atualizar ou deletar um registro.

Para cada uma das collections utilziadas no projeto, temos um arquivo model correspondente, alguns desses models (Os que são usados no CMS), possuem um método _update e um método _create, para fazer um parse do vem dos controllers antes de salvar os Dados.

Os arquivos que estão no diretório da API, são os que tem o mapeamento da API.

## Endpoints

```shell
GET /api/v1/cart HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/CartController.php*
```
Método

```shell
pending_payment_products()
```

Esse método pega os dados do carrinho do usuário, junta todas as informações do produto e retorna uma lista com as informações do catálogo da Oi e com os complementos de imagem e descrição feitos no CMS para o usuário. Esse endpoint retorna apenas produtos com status de `waiting` (produtos que ainda não foram pagos)

---

```shell
POST /api/v1/cart/{id} HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/CartController.php*
```
Método

```shell
add_item($id)
```

Esse adiciona um produto no carrinho

---

```shell
POST /api/v1/cart/domains?planId={id} HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
{
  "ID_PRODUTO":
  [
    "dominio.com"
  ]
}
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/CartController.php*
```
Método

```shell
add_domain_item()
```

Esse adiciona um produto no carrinho, apenas produtos do tipo domínio ou Oi Sites, o parametro `planId` na url é opcional.

---

```shell
POST cart/remove/{id} HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/CartController.php*
```
Método

```shell
delete_item($id)
```

Esse remove um produto do carrinho

---

```shell
POST cart/payment-product/{id} HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/CartController.php*
```
Método

```shell
pay_an_item($id)
```

Esse endpoint atualiza o status do produto para `paid` é chamado após o pagamento de um produto

---

```shell
GET cart/cart_payment HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/CartController.php*
```
Método

```shell
all_products()
```

Esse método pega os dados do carrinho do usuário, junta todas as informações do produto e retorna uma lista com as informações do catálogo da Oi e com os complementos de imagem e descrição feitos no CMS para o usuário. Esse endpoint retorna todos os produtos do carrinho do usuário, com status `waiting` e com status `paid`. 

---

```shell
POST /api/v1/discount-coupons HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
{
	"coupon-value": 1010
}
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/DiscountCouponsController.php*
```
Método

```shell
store(Request $request)
```

Além das validações para saber se o código do cupom é válido, se está dentro do período de uso, a lógica do método é adicionar ao carrinho do usuários as informações do produto com desconto, exibindo para ele o novo produto, também é feita uma exclusão do produto do carrinho da Oi e adicionado o novo produto.

---

```shell
POST /api/v1/cross-selling HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/CrossSellingController.php*
```
Método

```shell
index()
```

Esse endpoint retorna para o usuário uma lista de produtos sugeridos com até 2 níveis, com base no que o usuário acaba de comprar.

---

```shell
GET /api/v1/checkout/summary HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/SummaryController.php*
```
Método

```shell
index()
```

Esse endpoint retorna para o usuário uma lista de produtos pagos com as descrições cadastradas no CMS e com os dados de compra da API da Oi

---

```shell
POST /api/v1/sessions/new HTTP/1.1
Host: HOST_URL
Content-Type: application/json
Cache-Control: no-cache
Cookie:ckCarrinhoVendas=8510fd2bd83b8f072efb57b3e135bc14b0770e69;ckOnline=8510fd2bd83b8f072efb57b3e135bc14b0770e69;
{
 'login': LOGIN_USUARIO,
 'senha': SENHA_USUARIO,
 'isClientePPZ': false
}
```

Esse endpoint chega no arquivo

```shell
*ROOT/app/Http/Controllers/ApiV1/SessionsController.php*
```
Método

```shell
createSession()
```

Esse endpoint é chamado sempre após o login ou após o cadastro, para atualizar o carrinho do usuário.

[1]: https://secure.php.net/
[2]: https://laravel.com/
[3]: https://www.apache.org/
[4]: https://www.nginx.com/resources/wiki/
[5]: https://getcomposer.org/
