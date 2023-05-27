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

start your first container, try:
```bash
lxc launch ubuntu:22.04
```

can accept all defaults
```bash
lxd init 
```


If this is your first time running LXD on this machine, you should also run: lxd init

Or for a virtual machine: lxc launch ubuntu:22.04 --vm

```bash
lxd init 
```
