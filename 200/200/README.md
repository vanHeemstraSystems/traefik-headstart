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
      - ./data/traefik:/etc/traefik
    restart: unless-stopped
```
/containers/traefik/sample.docker-compose.yml

Let’s unpack this, as there’s a few subtle things going on here.

The docker socket is bound the container read-only, so Traefik only has read-only access to Docker, for slightly increased security.

I intentionally mount a directory in rather than just the traefik.yml to handle future expansion like [TLS certificates](https://theorangeone.net/posts/hello-world-with-traefik/#tls). Make sure the configuration file made in the previous section is named ```traefik.yml``` inside the ```containers/traefik/data/``` directory.

For ease, I’ve also set ```network_mode: host```. This means Traefik binds directly to ports on the host. The primary reason is because it allows Traefik to communicate with the upstream containers more easily and without defining a custom bridge network.
