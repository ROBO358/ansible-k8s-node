# ansible-k8s-node

## Lint

lint(offline)

```sh
docker run -v `pwd`:/root/workstation --rm registry.hub.docker.com/pipelinecomponents/ansible-lint:latest ansible-lint /root/workstation --offline
```

Rewrite to recommended settings
```sh
docker run -v `pwd`:/root/workstation --rm registry.hub.docker.com/pipelinecomponents/ansible-lint:latest ansible-lint /root/workstation --offline --fix
```

## Deploy

```sh
export ANSIBLE_CONFIG=$(pwd)
ansible-galaxy collection install community.general
ansible-playbook --ask-become-pass -i inventories/master/hosts.yaml init-k8s-cluster.yaml
ansible-playbook --ask-become-pass -i inventories/master/hosts.yaml join-master-k8s-cluster.yaml
ansible-playbook --ask-become-pass -i inventories/worker/hosts.yaml join-worker-k8s-cluster.yaml
```

## Use

```sh
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## Reset

```sh
ansible-playbook --ask-become-pass -i inventories/master/hosts.yaml -i inventories/worker/hosts.yaml reset-master.yaml
```
