# 200 - Create Traefik container

Now that we have a Traefik configuration file, we need to have a Traefik. For this, I use ```docker-compose``` to create a container configuration:

```
version: "2.3"

services:
  traefik:
    image: traefik:v2.2.11
    network_mode: host
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./traefik:/etc/traefik
    restart: unless-stopped
```
/containers/traefik/sample.docker-compose.yml


