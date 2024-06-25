# Docker-Swarm-Dashboard

- Iniciar o Swarm na Aplicação Docker

```sh
docker swarm init --advertise-addr + "ip da sua placa de rede" 
```

- Subir serviços no Swarm

```sh
docker stack deploy -c docker-swarm2.yml app
```

- Derrubar serviços no Swarm

```sh
docker stack rm app
```

- Ver serviços em execução

```sh
docker service ls
```

- Ver containers em execução

```sh
docker stats
```

- Entrar em um container:

```sh
# primeiro obtenha o id do container, pode ser via 'docker stats'
# com o id em mãos substitua '{id}' pelo id obtido
docker exec -it {id} bash
```

- URL's para acessar os serviços:

```sh
http://localhost:8080/ # WordPress
http://localhost:3000/ # Grafana, adicionar a url do Prometheus nas databases e ao criar o dashboard adicionar as metricas que deseja
http://localhost:9090/ # Prometheus
http://localhost:8081/ # CAdvisor
```

- Conectar o WordPress com o Redis:
    - Adicione o plugin "Redis Object Cache" no WordPress
    - Acesse o container do WordPress com:
        ```sh
        docker exec -it {id_do_container_wordpress} bash
        ```
    - Atualize o apt-get e baixe o nano:
        ```sh
        apt-get update && apt-get install nano
        ```
    - Abra o arquivo wp-config.php com o nano
    - Procure a linha "/* That's all, stop editing! Happy publishing. */" e adicione o codigo abaixo:
        ```sh
        define('WP_CACHE', true);define('WP_REDIS_HOST', 'redis');define('WP_REDIS_PORT', 6379);
        ```
    - Salve o arquivo e ative o cache de objeto no WordPress
