# Docker Nac!
> Subindo Front-end e Back-end com Docker :)

## Passos

### Clone

Primeiramente, precisamos clonar o projeto

```docker
  $ git clone https://github.com/MrBife/php-sample-app php-sample-app
  $ cd php-sample-app
```

### Build

Agora para o processo de Build para gerarmos nosso Container

```docker
  $ cd frontend
  $ docker build . -t front-php:*tag*
```
### Run

Agora iniciamos o container

```docker
  $ docker run -d -p 8000:8000 --rm -name front front-php:*tag*
```

### Consulta

Utilize este comando para conseguir identificar como estao seus containers

```docker
  $ docker ps -a
```


◔ ⌣ ◔
