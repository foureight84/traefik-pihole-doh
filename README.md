# Docker Swarm Pi-hole with DoH proxy support

### Stack overview

- Mangement Stack (mgmt)
  - Traefik - reverse proxy and load balancer
  - Portainer - Web UI Docker management tool
  - Whoami - Tiny Go webserver that prints os information and HTTP request to output
- Cloudflare DNS Stack (dns-cloudflare-doh)
  - Cloudflared DoH Proxy
  - Pi-hole DNS adblocker
- Unbound DNS Stack (dns-unbound)
  - Unbound recursive dns
  - Pi-hole DNS adblocker

My write up to get up and running https://blog.foureight84.com/swarm-your-pihole/
