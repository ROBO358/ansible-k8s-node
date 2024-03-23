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
ansible-playbook --ask-become-pass -i inventories/ym/hosts.yaml -l master deploy-node.yaml
```
