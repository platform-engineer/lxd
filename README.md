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


show container info
```bash
lxc info ubuntu
```

check list container
```bash
lxc list
```

start your first container, try:
```bash
lxc launch images:ubuntu/focal ubuntu
```




create snapshot
```bash
lxc snapshot ubuntu mysnap1
```


restore snapshot
```bash
lxc restore ubuntu mysnap1
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


set autostart
```bash
lxc config set ubuntu boot.autostart 1
lxc config set ubuntu limits.memory 4GB
```

```
lxc config show ubuntu
```


## Network

show interfaces

```
ip a
```


```
lxc profile show default
```


```
lxc profile create routed
```
    
lxc network attach my-network my-instance eth0
```
lxc network attach lxdbr0 ubuntu eth0
```


lxdbr0

lxc config device add <instance_name> eth0 nic nictype=bridged parent=br0
```
lxc config device add ubuntu eth0 nic nictype=bridged parent=br0
```

remove net
```
lxc config device remove ubuntu
```

net.ipv4.conf.<parent>.forwarding=1

```
net.ipv4.conf.lxd.forwarding=1    
```
    
lxc launch ubuntu: mycontainer --profile default

lxc launch ubuntu --profile default --profile routed
    
add
```
lxc config device add ubuntu eth0 nic nictype=routed name=eth0 parent=enp2s0 vlan=100 ipv4.address=10.220.47.106
```


  
    
## INSTALL UI
    
```   
lxc config set core.https_address "[::]:8443"
```
    
+ [canonical/dotrun](https://github.com/canonical/dotrun#installation)
    
```    
sudo apt install docker    
sudo apt install -y python3-pip
sudo pip3 install -y  dotrun
```
    
    
```    
git clone https://github.com/canonical/lxd-ui.git
cd lxd-ui
dotrun
sudo lxc config trust add keys/lxd-ui.crt
```    
    
