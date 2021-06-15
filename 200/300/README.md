# 300 - Test if Traefik is Accessible

Now we’ve got a Traefik configuration, and a docker configuration to run it, we can start Traefik and check it’s all working. Once the container has been downloaded and started, Traefik is running, congratulations!

If you browse to either ports 80 or 443, you’ll be met with a 404 page, this is normal. This happens because there’s no router matching the request - We’ll fix that later.

Whilst we only defined 2 entrypoints, Traefik actually defines an additional one, on port 8080. This is used by default for the dashboard but can be used by your applications if you want, or disabled entirely. If you browse to port 8080 now, you’ll be met by the Traefik dashboard.


Traefik dashboard

The dashboard shows which entrypoints, routers, middleware and services are active, and how they’re configured. This is an incredibly powerful tool for debugging what’s going on with Traefik, and which services and routes it’s picking up on.
