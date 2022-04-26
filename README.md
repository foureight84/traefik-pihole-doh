# Docker Swarm Pi-hole with DoH proxy support using Cloudflare or local recursive DNS using Unbound

### Stack overview

- Mangement Stack (mgmt)
  - Traefik - reverse proxy and load balancer
  - Portainer - Web UI Docker management tool
  - Whoami - Tiny Go webserver that prints os information and HTTP request to output
- Cloudflare DNS Stack (dns)
  - Cloudflared DoH Proxy
  - Pi-hole DNS adblocker
- Unbound DNS Stack (dns-unbound)
  - Unbound recursive dns
  - Pi-hole DNS adblocker
- Wireguard
  - Uses all-in-one Wireguard container and Web Management UI: https://github.com/WeeJeWel/wg-easy. There are several solutions but this seems to be the most robust.
  - update `WG_HOST` (public ip / A record), `PASSWORD`, `WG_DEFAULT_DNS` (local Host IP of instance running Pi-hole)
  - `WG_PORT` currently set to 123 instead of default 51820 to decrease chance of port being blocked on foreign networks.
  - run `docker stack deploy -c wireguard\docker-compose.yaml vpn`
  - web management http://<host_ip>:51821
  - create NAT forwarding rule on firewall port 123/udp from WAN to destination port  51820 on `host_ip`. Don't for get to add a Hairpin NAT rule as well for always on VPN (when connected in network).
  - **NOTE:** At the time of writing (4/24/2022) Portainer does not support cap_add flags in swarm mode even though support has been added to Docker enginer since 20.10.0. A work around can be found here https://github.com/fopina/docker-portainer-capability-manager#portainer-capability-manager. However, I have not been able to get Wireguard working while sitting behind Traefik (and probably not a good idea anyway).

My write up to get up and running with cloudflare https://blog.foureight84.com/swarm-your-pihole/ or with Unbound https://blog.foureight84.com/pi-hole-recursive-dns/
