# Local DNS server using Unbound

## Running in docker

```sh
docker run -v $(pwd)/custom.conf:/etc/unbound/custom.conf.d/custom.conf -p 5353:53/tcp -p 5354:53/udp klutchell/unbound:main
```

## Testing

```sh
dig grafana.homelab.com @localhost -p 5354
```
