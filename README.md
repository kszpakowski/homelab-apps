# Homelab app of apps

## Sealing secrets

```sh
SECRET_NAME=...
SECRET_NS=...
SECRET_KEY=...
SECRET_VALUE=...
kubectl create secret generic $SECRET_NAME --from-literal=$SECRET_KEY='$SECRET_VALUE' --dry-run -o yaml | kubeseal -o yaml --scope namespace-wide -n $SECRET_NS > $SECRET_NAME.yaml
```

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
