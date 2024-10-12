# Talos on Proxmox using Cluster-API (CAPI)

## Installing CAPI components using operator

### Install Cert-Manager

```sh
helm repo add jetstack https://charts.jetstack.io --force-update
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.14.4/cert-manager.crds.yaml
helm upgrade -i cert-manager jetstack/cert-manager --version v1.15.3--namespace cert-manager --create-namespace
```

### Install CAPI operator

If you need to re-download or update operator

```sh
curl -L https://github.com/kubernetes-sigs/cluster-api-operator/releases/download/v0.14.0/operator-components.yaml -o capi/operator/opreator.manifest.yaml
```

### Install it initially

```sh
kubectl apply -f capi/operator/
```

### Install core components

```sh
kubectl apply --server-side -f capi/providers/ipam-in-cluster
```

```sh
kubectl apply --server-side -f capi/providers/infra-proxmox
```

### Install Talos provider(s)

```sh
kubectl apply --server-side -f capi/providers/bootstrap-talos
```

```sh
kubectl apply --server-side -f capi/providers/controlplane-talos
```
