# 100 - Fundamentals

Traefik has three fundamental concepts: Entrypoints, Routers and Services.

Entrypoints define which ports and interfaces Traefik listens on for traffic. Generally you’d want one for port 80 and another for 443. Notice there’s nothing about protocols here, entrypoints can accept any protocol supported by Traefik, at the same time: HTTP, HTTPS, TCP and UDP.

Routers are what listen to entrypoints, and match domains and paths to applications. A route has a rule which identifies it, a service, and a set of middleware.

Services are your applications to route traffic to. A service may be a single container, or multiple in a load-balancing set up. Services can be either HTTP, TCP or UDP.

![image](https://user-images.githubusercontent.com/12828104/122052058-8e16dd00-cde5-11eb-81b3-7007cb9e4b91.png)

There is a 4th fundamental: Middleware. Middleware run in between a router and service, and can modify the request or response however they see fit. Traefik has a number of useful ones built in for adding headers, redirecting, rate limiting and more. To get started, you don’t really need to worry about them, but they’ll be useful as you deploy more applications.
