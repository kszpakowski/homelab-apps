# Homelab app of apps

## How to reinstall Traefik

To reinstall k3s bundled traefik first delete helm chart resources from kube-system namespace

```sh
kubectl -n kube-system delete helmchart traefik
kubectl -n kube-system delete helmchart traefik-crd
```

Then login to the node and re-apply traefik resources

```sh
kubectl apply -f /var/lib/rancher/k3s/server/manifests/traefik.yaml
```
