# OpenEx Docker deployment

OpenEx can be deployed using the *docker-compose* command.

## Pre-requisites

To install OpenEx using Docker, you will need the docker-compose command, you can install it using:

```bash
$ sudo apt-get install docker-compose
```

## Clone the repository

```bash
$ mkdir /path/to/your/app && cd /path/to/your/app
$ git clone https://github.com/OpenEx-Platform/docker.git
$ cd docker
```

## Configure the environment

Before running the `docker-compose` command, the `docker-compose.yml` file must be configured.  Two ways to do that:

- Use environment variables as it is proposed and you have an exemple in the `.env.sample` file (ie. `ADMIN_TOKEN=${ADMIN_TOKEN}`).
- Directly set the parameters in the `docker-compose.yml`.

 Whether you are using one method or the other, here are the mandatory parameters to fill:

```bash
APP_SECRET=ChangeMe # Valid UUIDv4
ADMIN_TOKEN=ChangeMe # Valid UUIDv4
COOKIE_SECURE=false
AUTH_LOCAL_ENABLE=true
MAILER_URL=smtp://username:password@smtp.changeme.com
SPRING_MAIL_HOST=smtp.changeme.com
SPRING_MAIL_PORT=25
SPRING_MAIL_USERNAME=ChangeMe@domain.com
SPRING_MAIL_PASSWORD=ChangeMe
SPRING_MAIL_PROPERTIES_MAIL_SMTP_SSL_TRUST=*
SPRING_MAIL_PROPERTIES_MAIL_SMTP_SSL_ENABLE=false
SPRING_MAIL_PROPERTIES_MAIL_SMTP_AUTH=false
SPRING_MAIL_PROPERTIES_MAIL_SMTP_STARTTLS_ENABLE=false
```

## Run

### Using single node Docker

You can deploy without using Docker swarm, with a the `docker-compose` command. After changing your `.env` file, just type:

```bash
$ sudo docker-compose up -d
```

### Using Docker swarm

In order to have the best experience with Docker, we recommend using the Docker stack feature. In this mode you will have the capacity to easily scale your deployment. If your virtual machine is not a part of a Swarm cluster, please use:

```bash
$ sudo docker swarm init
```

Then, you have to put your environment variables in the `/etc/environment` and then:

```bash
$ sudo source /etc/environment
$ sudo docker stack deploy --compose-file docker-compose.yml openex
```

You can now go to [http://localhost:8080](http://localhost:8080/) and log in with the default credentials:

- Login: admin@openex.io
- Password: admin

## Update

### Using single node Docker

```bash
$ sudo docker-compose stop
$ sudo docker-compose pull
$ sudo docker-compose up -d
```

### Using Docker swarm

For each of services, you have to run the following command:

```bash
$ sudo docker service update --force service_name
```

## Data persistence

If you wish your OpenEx data to be persistent while in production, you should be aware of the `volumes` section for `OpenEx` and `PostgreSQL` services in the `docker-compose.yml`.

Here is an example of volumes configuration:

```
volumes:
  pgsqldata:
    driver: local
    driver_opts:
      o: bind
      type: none
  openexdata:
    driver: local
    driver_opts:
      o: bind
      type: none      
```

## Memory configuration

OpenEx default `docker-compose.yml` file does not provide any specific memory configuration. But if you want to adapt some dependencies configuration, you can find some links below.

### OpenEx - Platform

OpenEx platform is based on Symfony 5 (PHP) and the main Docker container is running an Apache 2 server. This server runs with a memory limit of **512MB by default**.

You can find more information in the [official Apache 2 documentation](https://hub.docker.com/_/httpd)

### OpenEx - Player

OpenEx player is a JAVA process. In order to setup the JAVA memory allocation, you can use the environment variable `ES_JAVA_OPTS`.

The minimal recommended option today is -Xms1G -Xmx1G.

### PostgreSQL

PostgreSQL is the main database of OpenEx.

You can find more information in the [official PostgresQL documentation](https://hub.docker.com/_/postgres).
