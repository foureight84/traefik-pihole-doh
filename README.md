# Docker Swarm Pi-hole with DoH proxy support

### Stack overview

- Mangement Stack (mgmt)
  - Traefik - reverse proxy and load balancer
  - Portainer - Web UI Docker management tool
  - Whoami - Tiny Go webserver that prints os information and HTTP request to output
- DNS Stack (dns)
  - Cloudflared DoH Proxy
  - Pi-hole DNS adblocker and DHCP server

My write up to get up and running https://blog.foureight84.com/swarm-your-pihole/