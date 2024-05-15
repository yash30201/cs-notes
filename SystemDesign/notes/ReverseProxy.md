# Reverse Proxy

A reverse proxy is a server that sits in front of web servers and forward client request to those web servers. Reverse proxies are used to:
- Increase security
- Performance (sending requests to appropriate web servers for faster processing)
- Reliability (something like horizontal scaling)

# Seems like a Load Balancer right?

**Reverse Proxy**: This middleman intercepts requests, potentially modifies them, and then passes them on to the appropriate server.

**Load Balancer**: Distributes incoming requests across a pool of multiple servers with the sole aim of spreading out work and preventing a single server from being overwhelmed.

## Key Purposes of Reverse proxy

- **Security**: Hides the backend server structure, protecting from direct attacks.
- **Caching**: Storing and returning frequently asked content, saving a trip to the web server
- **Fetures**: Do things like compression, ssl handling, etc before sending the request to the web server.

## Key Purpose of Load Balancer
- **Scalability**: Allows you to handle more traffix by adding servers to the pool.
- **Availability**: Keeps the site running even if a server goes down (distributes the traffic to others evenly)
    - This!, this is a very stricking difference b/w this and reverse proxy.
- **Flexibility**: Can use different algorithms to choose the best serve (though, reverse proxy can do this too)

## Overlap !

- If requirements are handling security, caching, a single web server, **then Reverse Proxy is enough**.
- If there are multiple servers and traffic distribution is required, **then Load Balancer**.
- If complex needs (high traffic site with complex preprocessing), then it makes sense to get a mordern load balancer with a combination of both.

## Exmples

- **Reverse Proxies**: NginX, HAProxy
- **Load Balancers**: NginX (again!!), AWS Elastic Load Balancing (ELB), Google Cloud Load Balancing ([link](https://cloud.google.com/load-balancing/docs/))
