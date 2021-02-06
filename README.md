# personal-k8s-cluster

Once K3S/K8S is deployed to all nodes, jenkins pipelines should be run in the following order

- kubernetes
- metallb: home-k3s-metallb
- nginx: home-k3s-nginx
- cert-manager: home-k3s-cert
