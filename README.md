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


show container info
```bash
lxc info ubuntu
```


create snapshot
```bash
lxc snapshot ubuntu mysnap1
```



start a virtual machine: 
```bash
lxc launch ubuntu
```

go to the shell
```bash
lxc shell ubuntu
```

check whether you have sudo privileges or not, you can launch the following command.
```
sudo -l
```

changee a password for root user
```bash
sudo passwd root
```

check hostname
```bash
hostnamectl
```


check IP adress
```
ifconfig
```

if ont exist, install:
```
apt install net-tools
```


To check that this is actually the case, you can run the “ssh” command with the “-V” option.
```
ssh -V
```

if not installed:
```        
sudo apt-get install openssh-server
```


change username or/and password
```bash
whoami
passwd
```


install app in container
```bash
lxc exec ubuntu -- apt install -y ubuntu-desktop
```

install app in container
```bash
lxc exec ubuntu -- apt install -y firefox
```

search
```bash
lxc image list images
lxc image list images: ubuntu focal
```

restart
```bash
lxc restart ubuntu
```
