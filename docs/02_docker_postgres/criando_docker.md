Geralmente, quando estamos começando uma aplicação, ou quando queremos rodar a aplicação de alguém localmente, precisamos configurar o banco de dados, sendo necessário instalar ele na máquina. Há também casos em que já temos algum banco rodando localmente e precisamos criar um novo, isso acaba dificultando a configuração.
E por falar em configuração, oque acontece quando fazemos muitas configurações em nosso banco local e depois temos que rodar ele em outra máquina? Temos que configurar tudo novamente?
Felizmente, com o surgimento dos containers, isso se torna muito mais fácil, uma vez que nosso banco de dados se resume a uma imagem, que roda em um container juntamente com todas as configurações e dependências. Isso permite rodar nosso banco em diferentes ambientes, sem ter que se preocupar com configuração, compatibilidade, etc.
Neste exemplo, irei mostrar como rodar um banco de dados Postgres utilizando o Docker, no final, mostrarei como mapear um volume para que nossos dados fiquem gravados na máquina.

Esta é a configuração final:

```yml
version: '3'

services:
  teste-postgres-compose:
    image: postgres
    environment:
      POSTGRES_PASSWORD: "@Admin2020!"
    ports:
      - "15432:5432"
    volumes:
      - /home/mpi/volumes-docker:/var/lib/postgresql/data 
    networks:
      - postgres-compose-network
      
  teste-pgadmin-compose:
    image: dpage/pgadmin4
    environment:
      PGADMIN_DEFAULT_EMAIL: "palin@mail.com"
      PGADMIN_DEFAULT_PASSWORD: "@Admin2020!"
    ports:
      - "16543:80"
    depends_on:
      - teste-postgres-compose
    networks:
      - postgres-compose-network

networks: 
  postgres-compose-network:
    driver: bridge

```

Basta colocar este conteúdo dentro do arquivo docker-compose.yml
e rodar:

```
docker-compose up -d
```

-d = deatach para o processo rodar em background

No arquivo acima foram criados a rede "postgres-compose-network" que interliga os containeres do postgres e do pgadmin:

```
backend/app$ docker network ls
NETWORK ID     NAME                               DRIVER    SCOPE
f3e1bb9671a5   backend_postgres-compose-network   bridge    local
```

Como o docker-compose.yml está dentro do diretório **backend** e executamos o comando docker-compose up -d dentro do diretório o nome que ficou foi: **backend_postgres-compose-network**

## Para criar uma network na mão

Network (rede) são pontes de comunicação que possibilitam à contêineres uma conexão entre eles. Geralmente, criasse uma network quando dois ou mias contêineres têm uma relação e comunicam-se. Portanto, para este caso crie uma network chamada **backend_postgres-compose-network** utilizando o comando abaixo:

```
docker network create -d bridge backend_postgres-compose-network
```

# Como seria se criássemos tudo na mão?

https://medium.com/@felixgilioli/como-rodar-um-banco-de-dados-postgres-com-docker-6aecf67995e1

https://dev.to/devbaraus/postgresql-docker-5c3n

Por padrão, o Postgres roda na porta 5432, mas isso fica disponível apenas dentro do container, para permitir que ele acessado pela máquina local, precisamos um mapping da porta interna, para porta externa. Fazemos isso com o parametro -p, logo após, indicamos uma porta local e para qual porta deve redirecionar, por exemplo, -p 5432:5432.

Para podermos definir vários dockers de postgres em geral colocamos uma porta aleatória da máquina local, ex: 15432 e mapeamos para a porta 5432 com o comando -p 15432:5432

Para definirmos qual a senha do banco, devemos alterar uma variável de ambiente, -e POSTGRES_PASSWORD=suasenha.

Isso é o suficiente para podermos rodar nosso banco, agora, iremos subir o container com o comando run, passando as configurações que vimos acima.

```
docker run -p 15432:5432 -e POSTGRES_PASSWORD=1234 postgres
```


