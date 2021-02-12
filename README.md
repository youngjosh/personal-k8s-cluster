# personal-k8s-cluster

Once K3S/K8S is deployed to all nodes, jenkins pipelines should be run in the following order

- kubernetes
- metallb: home-k3s-metallb
- nginx: home-k3s-nginx
- cert-manager: home-k3s-cert

# To install K3S on a new agent node

`curl -sfL https://get.k3s.io | K3S_URL=myserverurl K3S_TOKEN=mynodetoken INSTALL_K3S_VERSION=versionum sh -`

At time of writing, the K3S url is 192.168.1.22:6443. 
Node token can be found by performing `sudo cat /var/lib/rancher/k3s/server/node-token` on master node.
Version is found from kubectl get nodes. Currently v1.20.0+k3s2

# Troubleshooting

## Node Restart

If the node is stuck in "NotReady" after power loss
-SSH into node and run k3s agent --token CLUSTER_TOKEN --server SERVER_IP