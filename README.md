# OpenEx Docker deployment

OpenEx could be deployed using the *docker-compose* command.

## Clone the repository

```bash
$ mkdir /path/to/your/app && cd /path/to/your/app
$ git clone https://github.com/OpenEx-Platform/docker.git
$ cd docker
```

### Config


## Data persistence

If you wish your OpenEx data to be persistent in production, you should be aware of the  `volumes` section for `PostgreSQL` service and `OpenEx` platform in the `docker-compose.yml`.

Here is an example of volumes configuration:

```yaml
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
