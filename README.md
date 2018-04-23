> Este projeto segue as especificações requeridas do repositório ->  **[Sistemas para Internet - SecDevOps](https://github.com/fiapsecdevops/php-sample-app)**.

<div align="center">
  <img alt="fiap-logo" src="https://www.futurecom.com.br/content/dam/Informa/futurecom/images/conteudo-gratuito/fiap.png" style="max-height: 50px; width:100; height: auto; max-width:100%; margin-top: 50px; margin-bottom: 20px" />
</div>

<div align="center">
  <img alt="fiap-logo" src="https://cdn-images-1.medium.com/max/792/1*7a8Qffxkg7WuePBZUebYSw.png" style="max-height:100px; width:100; height: auto; max-width:100%; margin-top: 50px; margin-bottom: 20px" />
</div>

<div align="center">
  <strong>Criação de uma aplicação no formato "CRUD" executada em containers com base na linguagem "PHP" e no banco de dados "MySQL"</strong>
</div>

## Quickstart 🏃‍
Primeiro, tenha certeza que o [Docker](https://www.docker.com/) esteja instalado corretamente.

Para saber a versão instalada, no terminal:
```bash
docker -v
```
---

## Front-End

#### `Build da Imagem`

Iremos Buildar uma Imagem:
```bash
docker build . -t frontend-php:0.0.1
```
* **docker build** é um comando CLI do Docker para gerarmos containers.
* **-t** significa Tag, portanto conseguimos futuramente identifica-lo melhor.
* **frontend-php** é o nome do projeto que estamos dando (é de sua escolha).
* **:0.0.1** é a versão que estamos dando ao projeto.

##### O que é uma imagem?

Uma imagem Docker são blocos de containers em execução. Para executar um container é preciso construir a imagem inicialmente.


<div align="center">
  <img alt="explicacao-docker" src="https://i1.wp.com/blog.docker.com/wp-content/uploads/011f3ef6-d824-4d43-8b2c-36dab8eaaa72-2.jpg?w=650&ssl=1" style="max-height:300px; width:100; height: auto; max-width:100%; margin-top: 50px; margin-bottom: 20px" />
</div>

##### O que é e o que tem dentro do Dockerfile?
Dockerfile é um arquivo com o padrão Docker onde nós colocamos nossos comandos para podermos automatizar deploys. Nele podemos buildar uma imagem do Docker e executar instâncias de containers. É de extrema importancia a ordem em que iremos colocar os códigos, o Dockerfile é lido de baixo para cima.

```bash
FROM php:7.2-apache
```
* Esta dizendo qual imagem você escolheu com sua versão respectivamente. A imagem vem do [DockerHub](https://hub.docker.com/), existem diversas imagens prontas... É possível criar sua própria imagem e subir ela para sua necessidade.

```bash
RUN docker-php-ext-install mysqli
```
* Podemos instalar extensões, neste caso é uma extensão que liga o PHP com MySql.

```bash
WORKDIR /var/www/html/
```
* Diretório de execução.

```bash
COPY . /var/www/html/
```
* Copia todo o conteúdo.

#### `Para verificar se a imagem foi realmente criada:`
```bash
docker images
```
Você pode observar detalhes de outras imagens que você já criou utilizando este comando.

#### `Executando nosso Container`

Para executarmos nosso Container com nossa aplicação:
```bash
docker run -d -p 80:80 --rm --name frontend frontend-php:0.0.1
```

* **docker run** comando CLI do Docker.
* **-d** deixa o container executando em segundo plano.
* **-p** define a porta utilizada, seguida de porta base para porta destino("x":"x").
* **--rm --name** nome do container.

#### `Verificar se está executando`

Utilize um comando CLI do Docker:
```bash
docker ps
```
Ele irá mapear todos os containers que estão rodando.

---

## Back-End

#### `Utilizando imagem PHP com Apache e MySQL`

Iremos utilizar o terminal e o Docker CLI para pegarmos as imagens do PHP com Apache e MySQL.

Tenha certeza que esteja no diretório do Back-end para executar estes comandos:

```bash
docker pull php:7.2-apache
```
* Estamos pegando o PHP com Apache.

```bash
docker pull mysql:latest
```
* E agora o MySQL na sua última versão.

#### `Build da Imagem do MySQL`

```bash
docker build -t db:0.0.1
```
* **-t** significa Tag, portanto conseguimos futuramente identifica-lo melhor.
* **:0.0.1** é a versão que estamos dando ao projeto.

#### `Para verificar se a imagem foi realmente criada:`
```bash
docker images
```
Você pode observar detalhes de outras imagens que você já criou utilizando este comando.

#### `Executando nosso Container`

Para executarmos nosso Container com nossa aplicação:
```bash
docker run -d -e MYSQL_DATABASE=demo -e MYSQL_ALLOW_EMPTY_PASSWORD=yes --name backend db:0.0.1
```

* **docker run** comando CLI do Docker.
* **-d** deixa o container executando em segundo plano.
* **-e** é o uso da nossa variável.
* **MYSQL_DATABASE=demo** nome do nosso banco de dados.
* **MYSQL_ALLOW_EMPTY_PASSWORD=yes** permite o uso de senha vazia.
* **--name** nome do container.

#### `Verificando o Container`
```bash
docker exec -ti backend mysql -u root -p
```

* **docker exec** executa a função.
* **-ti backend mysql** especifica qual projeto e qual tecnologia.
* **-u root -p** utiliza o padrão de portas para conectar o banco.

---

## Conectando Front com o Back
Por fim, linkamos nossos dois projetos que estão sendo executados em containers:

```bash
docker run -d -p 80:80 --name frontend --link backend frontend:0.0.1
```

* **--link** conecta dois containers, fazendo uma ligação entre os dois.
---
## O que nós aprendemos?
* **Criamos um Container de um projeto**, entendemos como eles funcionam e como executamos.
* **Utilizamos imagens para a construção de Containers** utilizando DockerHub, dando asas para criar infinitos projetos com imagens de lá.
* **Linkamos os projetos de Containers diferentes** e agora tudo faz sentido, tá tudo junto e funcionando em sincronia
* **Subimos um projeto completo em Docker!** pera... É isso mesmo? Olocoo meu! :D

Sério que você curtiu? Que foda! ^^

<a href="https://docs.docker.com/">A Documentação do Docker tem muita coisa maneira!</a>

◔ ⌣ ◔
