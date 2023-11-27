# Deployment with Traefik

## Agenda

- forward proxy vs reverse proxy
- load balancer
- deployment environment
- what is traefik ?
- deployment setup

## Proxy

Proxy comes from a contracted form of the Middle English word procuracie (meaning “procuration”).
A proxy may refer to a person who is authorized to act for another or it may designate the
function or authority of serving in another’s stead. In the latter sense, it generally is
preceded by the word by (“vote by proxy”).

### Forward proxy

<img src="../images/forward-proxy.png" height="328" width="416" alt="forward-proxy">

### What is a forward proxy?

A forward proxy is a proxy that is used by clients to access other servers.

Benefits of using a forward proxy:

- Ann additional layer of security and anonymity
- Caching
- Content filtering
- Bypassing geo-restrictions

### Reverse proxy

<img src="../images/reverse-proxy.png" height="328" width="416" alt="reverse-proxy">

### What is a reverse proxy?

A reverse proxy is a type of proxy server that retrieves resources on behalf of a client from one or more servers. 
These resources are then returned to the client as though they originated from the proxy server itself.


Benefits of using a reverse proxy:

- Load balancing
- Web acceleration
- Security and anonymity
- SSL termination
- Serve static content
- Compression
- Caching

## Load balancer

<img src="../images/load-balancer.png" height="255" width="615" alt="load-balancer">

### What is a load balancer?

A load balancer is a device that acts as a reverse proxy and distributes network or application traffic across a
number of servers.

### Why use a load balancer?

- High availability
- Scalability
- Security
- SSL termination
- Session persistence
- Content-based routing
- Health checks
- Caching

## Traefik




