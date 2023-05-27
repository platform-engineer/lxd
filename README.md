# lxd
first steps on ubuntu, lxd, ...

## install lxd
```bash
snap install lxd
```

check
```bash
snap list
```


## add user to the group
```bash
sudo usermod -aG lxd $(whoami)
```
check
```bash
groups
```


## create container

check
```bash
which lxc
```

check the list of remote servers
```bash
lxc remote list
```


If this is your first time running LXD on this machine, you should also run:
```bash
sudo lxd init 
```

result yaml file
```yaml
config: {}
networks:
- config:
    ipv4.address: auto
    ipv6.address: auto
  description: ""
  name: lxdbr0
  type: ""
  project: default
storage_pools:
- config: {}
  description: ""
  name: default
  driver: dir
profiles:
- config: {}
  description: ""
  devices:
    eth0:
      name: eth0
      network: lxdbr0
      type: nic
    root:
      path: /
      pool: default
      type: disk
  name: default
projects: []
cluster: null
```

check list container
```bash
lxc list
```

start your first container, try:
```bash
lxc launch images:ubuntu/focal ubuntu
```

start a virtual machine: 
```bash
lxc launch ubuntu:22.04 --vm
```


search
```bash
lxc image list images
lxc image list images: ubuntu focal
```

