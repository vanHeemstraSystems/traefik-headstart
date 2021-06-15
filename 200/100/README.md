# 100 - Configuring Traefik

Traefik configuration is split into 2 types. Static configuration lives in Traefik’s main configuration file. Dynamic configuration generally lives with the thing you’re routing traffic to, which in this case is docker containers.

To access the dashboard, you’ll need to enable it in traefik.yml. It’ll be incredibly useful later.

```
...
api:
  dashboard: true
  insecure: true
...  
```
/containers/traefik/data/sample.traefik.yml

Setting insecure means the dashboard is accessible to anyone and everyone on port 8080. For a production deployment, you’ll likely want to create your own router to add a layer of authentication, or just block the port with a firewall. But for now, this is fine.

We need to configure the entrypoints and communication to docker in traefik.yml also.

```
...
entryPoints:
  web:
    address: :80

  web-secure:
    address: :443
...    
```    
/containers/traefik/data/sample.traefik.yml

Configuration for entrypoints is incredibly simple. Here we define 2 entrypoints: web and web-secure, listening on ports 80 and 443 respectively.

Next we need to tell Traefik where it can find some providers. Providers are where Traefik’s dynamic configuration comes from, and tell it how to discover services, routers and middleware.

```
...
providers:
  docker:
    endpoint: unix:///var/run/docker.sock
    watch: true
    exposedByDefault: false
...    
```
/containers/traefik/data/sample.traefik.yml

Here we tell Traefik to communicate with docker using the docker socket. exposedByDefault makes the dashboard look cleaner, and prevents things accidentally being routable when we don’t want them to be. watch: true instructs Traefik to watch for changes to running containers, and automatically clean up or create routers and services as necessary, all without requiring a restart.

In sum:

```
api:
  dashboard: true
  insecure: true

entryPoints:
  web:
    address: :80

  web-secure:
    address: :443
    
providers:
  docker:
    endpoint: unix:///var/run/docker.sock
    watch: true
    exposedByDefault: false
```
/containers/traefik/data/sample.traefik.yml
