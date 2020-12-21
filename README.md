# 1. fastapi-simple-app-example

References: 

- https://alexvanzyl.com/posts/2020-05-19-fastapi-simple-application-structure-from-scratch/

- https://fastapi.tiangolo.com/tutorial/bigger-applications/


É um excelente artigo do Alexander van Zyl que resumir em português aqui para quem se interessar.


# 2. BAIXANDO E RODANDO O PROJETO

Dica para iniciante: - para quem está iniciando agora no mundo da programação e optou por aprender python, python para Web, API é necessário e fundamental que entendenta sobre Git.
Existem diversos locais que você pode iniciar o aprendizado. Segue alguns:
- https://terminalroot.com.br/git/
- https://jera.com.br/blog/6620/desenvolvimento/guia-do-dev-iniciante-introducao-ao-git
- https://kinsta.com/pt/base-de-conhecimento/que-github/
- https://helpdevs.net/2020/02/04/introducao-ao-git/

## 2.1. Clone o projeto para sua máquina

Clonando por SSH: git clone git@github.com:marcelopalin/fastapi-simple-app-example.git
Clonando por Https: git clone https://github.com/marcelopalin/fastapi-simple-app-example.git

## 2.2. Instalando as Dependências com Poetry

```
poetry install
```

Saída:

```
poetry install
Creating virtualenv app-uvxveFX1-py3.8 in /home/mpi/.cache/pypoetry/virtualenvs
Installing dependencies from lock file

Package operations: 46 installs, 0 updates, 0 removals

  • Installing markupsafe (1.1.1)
  • Installing mypy-extensions (0.4.3)
  • Installing pyparsing (2.4.7)
  • Installing six (1.14.0)
  • Installing typed-ast (1.4.1)
  • Installing typing-extensions (3.7.4.2)
  • Installing appdirs (1.4.4)
  • Installing attrs (19.3.0)
  • Installing click (7.1.2)
  • Installing dnspython (1.16.0)
  • Installing h11 (0.9.0)
  • Installing httptools (0.1.1)
  • Installing idna (2.9)
  • Installing mako (1.1.2)
  • Installing mccabe (0.6.1)
  • Installing more-itertools (8.2.0)
  • Installing mypy (0.770)
  • Installing packaging (20.3)
  • Installing pathspec (0.8.0)
  • Installing pluggy (0.13.1)
  • Installing py (1.8.1)
  • Installing pycodestyle (2.6.0)
  • Installing pydantic (1.5.1)
  • Installing pyflakes (2.2.0)
  • Installing python-dateutil (2.8.1)
  • Installing python-editor (1.0.4)
  • Installing regex (2020.5.7)
  • Installing sqlalchemy (1.3.16)
  • Installing starlette (0.13.2)
  • Installing toml (0.10.0)
  • Installing uvloop (0.14.0)
  • Installing wcwidth (0.1.9)
  • Installing websockets (8.1)
  • Installing alembic (1.4.2)
  • Installing autopep8 (1.5.2)
  • Installing black (19.10b0)
  • Installing email-validator (1.1.0)
  • Installing fastapi (0.54.1)
  • Installing flake8 (3.8.1)
  • Installing inflect (4.1.0)
  • Installing isort (4.3.21)
  • Installing psycopg2-binary (2.8.5)
  • Installing pytest (5.4.2)
  • Installing python-dotenv (0.13.0)
  • Installing sqlalchemy-stubs (0.3)
  • Installing uvicorn (0.11.5)

Installing the current project: app (0.1.0)
```

Obs: veja que seu ambiente virtual fica em:

```
Creating virtualenv app-uvxveFX1-py3.8 in /home/seu_usuario/.cache/pypoetry/virtualenvs
```

Ativando o ambiente (shell):

```
poetry shell
```

```
poetry shell
Spawning shell within /home/mpi/.cache/pypoetry/virtualenvs/app-lxvZgIHf-py3.8
. /home/mpi/.cache/pypoetry/virtualenvs/app-lxvZgIHf-py3.8/bin/activate
mpi@wsl2:~/github.com/fastapi-simple-app-example$ . /home/mpi/.cache/pypoetry/virtualenvs/app-lxvZgIHf-py3.8/bin/activate
(app-lxvZgIHf-py3.8) mpi@wsl2:~/github.com/fastapi-simple-app-example$ 
```

Perceba que seu prompt de comando fica parecido com este:

(app-lxvZgIHf-py3.8) mpi@wsl2:~/github.com/fastapi-simple-app-example$ 


# 3. Rodando a Aplicação pelo Docker

Requisitos: 

- docker instalado na sua máquina

Verificação:

```
docker --version
Docker version 20.10.0, build 7287ab3
```

```
docker-compose --version
docker-compose version 1.27.4, build 40524192
```

Atenção: Caso já tenha rodado antes a criação dos contâiners e deseja excluir tudo e recomeçar
você pode seguir o guia https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes-pt

No meu caso, meu ambiente de teste e não tenho nada a perder, mas se você tiver **não execute este comando** a menos que saiba o que está fazendo.


```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

Executando:

```
(app-lxvZgIHf-py3.8) mpi@wsl2:~/github.com/fastapi-simple-app-example$ docker stop $(docker ps -a -q)
62a9a24b9901
45e92e601d29
8276dedcd35d
(app-lxvZgIHf-py3.8) mpi@wsl2:~/github.com/fastapi-simple-app-example$ docker rm $(docker ps -a -q)
62a9a24b9901
45e92e601d29
8276dedcd35d
(app-lxvZgIHf-py3.8) mpi@wsl2:~/github.com/fastapi-simple-app-example$ 
```

Portanto, agora

```
docker container ps
```

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

Está tudo limpo.

## Criando a imagem e subindo o servidor

```
docker-compose up -d
```

# Executando o Projeto sem Docker

Para executar o projeto pela seguinte linha de comando, antes
certifique-se que o .env esteja com as configurações corretas de acesso ao banco de dados.
Também certifique-se de que seu banco de dados esteja rodando.

## Instalar o Postgres no seu Linux Ubuntu 20.04

```
sudo apt update
```

```
sudo apt install postgresql postgresql-contrib
```

```
$sudo /etc/init.d/postgresql status
13/main (port 5432): down

$ sudo /etc/init.d/postgresql start
 * Starting PostgreSQL 13 databas server                                                                                                                    
 
$ sudo /etc/init.d/postgresql status
13/main (port 5432): online
```

```
sudo netstat -plunt | grep postgres
[sudo] password for mpi: 
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN      10906/postgres
```

Você também pode executar o comando que quiser com a conta postgres diretamente com o sudo:

```
sudo -u postgres psql
```

# Criando o BD

```
create database meteorologia_db;
```

# Criando Usuário

```
create user admin with encrypted password 'sua_senha';
```

```
grant all privileges on database meteorologia_db to admin;
```

```
GRANT ALL ON ALL TABLES IN SCHEMA public TO admin;
```

## Como remover postgres 11 e 13 instalados

```
sudo /etc/init.de/postgres stop
```

```
sudo apt --purge remove pgdg-keyring postgresql postgresql-11 postgresql-13 postgresql-client-11 postgresql-client-13  postgresql-client-common postgresql-common postgresql-contrib
```

O procedimento de instalação criou uma conta de usuário chamada postgres que está associada ao role padrão do Postgres. Existem algumas maneiras de utilizar essa conta para acessar o Postgres. 


# Configurando o arquivo .env

```ini
# PostgreSQL com Docker utilize
# POSTGRES_SERVER=db
# Sem o Docker utilize
POSTGRES_SERVER=localhost 
POSTGRES_PORT=5432
POSTGRES_USER=admin
POSTGRES_PASSWORD=sua_senha
POSTGRES_DB=meteorologia_db

INSTALL_DEV=true
INSTALL_JUPYTER=true

# PgAdmin
PGADMIN_DEFAULT_EMAIL=admin@mail.com
PGADMIN_DEFAULT_PASSWORD=sua_senha
PGADMIN_LISTEN_PORT=8080
```

# Rodando o Servidor da API

Depois de ter instalado o poetry na sua máquina rode:

```
poetry install 
```
```
poetry shell 
```

# Rode a primeira migração para criar a tabela posts

```
alembic upgrade head
```

```
uvicorn app.main:app --reload
```

Acesse a url: http://localhost:8000/docs

Clique em Try Out e crie um post depois liste os posts.

# Como rodar o script no Docker

Antes não esqueça de criar o .env da seguinte maneira:

```ini
# PostgreSQL com Docker utilize
POSTGRES_SERVER=db
# Sem o Docker utilize
# POSTGRES_SERVER=localhost 
POSTGRES_PORT=5432
POSTGRES_USER=postgres
POSTGRES_PASSWORD=sua_senha
POSTGRES_DB=meteorologia_db

INSTALL_DEV=true
INSTALL_JUPYTER=true

# PgAdmin
PGADMIN_DEFAULT_EMAIL=admin@mail.com
PGADMIN_DEFAULT_PASSWORD=sua_senha
PGADMIN_LISTEN_PORT=8080
```

Outra coisa, o usuário do BD no .env deve ser o **postgres**

Em app/config.py comente a linha 35 
        # env_file = ".env"


```
docker-compose up -d
```

Saída:

Creating fastapi-simple-app-example_db_1 ... done
Creating fastapi-simple-app-example_pgadmin_1 ... done
Creating fastapi-simple-app-example_server_1  ... done

```
docker ps 
```

Você verá que está rodando o pgadmin na porta 8080 com o login que foi definido no seu arquivo .env
E a api está configura para a porta 80.

Portanto acesse a api e o pgadmin com as seguintes urls:

```
http://localhost/docs
```

```
http://localhost:8080/
```

```
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                                     NAMES
02edee6b376b   dpage/pgadmin4   "/entrypoint.sh"         2 minutes ago   Up 2 minutes   80/tcp, 443/tcp, 0.0.0.0:8080->8080/tcp   fastapi-simple-app-example_pgadmin_1
473fad4638a5   postgres:12      "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   5432/tcp                                  fastapi-simple-app-example_db_1
```

# Criando uma configuração no PgAdmin

Com o botão direito em Server escolha "Create Server" em Connection coloque **db** que é o nome do contâiner com o usuário **postgres** e senha definida no .env.

Ao se conectar em local -> Databases -> meteorologia_db você verá a tabela **posts**


# Comandos Úteis Docker

```markdown
## Containers

- Abrir um shell em um container em execução:
	- `docker exec -t -i <container_id> <shell>`

## Limpeza

- Excluir containers com status equivalente a Exited:
	- `docker rm -v $(docker ps -a -q -f status=exited)`
- Remover imagens não utilizadas do cache local:
	- `docker rmi $(docker images -f "dangling=true" -q)`
- Limpar o diretório de volumes (vsf) do docker:
	- `docker run -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker:/var/lib/docker --rm martin/docker-cleanup-volumes`

# Info

docker info

```

