# Install Vagrant + VirtualBox provider on Fedora Workstation

Host: Fedora Workstation 37  
Guest: Ubuntu 2210

## Prepare your computer

Step1: disable secure boot.

Next [based on this message](https://discussion.fedoraproject.org/t/what-is-the-best-way-of-installing-virtualbox-on-f37/74926) :

```sh
$ sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
$ sudo dnf install -y VirtualBox
```

Install Vagrant `v2.3.4` (version not provider by default Fedora repository):

```
$ sudo dnf install -y dnf-plugins-core
$ sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/fedora/hashicorp.repo
$ sudo dnf -y install vagrant
```


```sh
$ vagrant --version
Vagrant 2.3.4
```

```sh
$ VBoxManage --version
7.0.6_rpmfusionr155176
```

```sh
$ cat <<EOF > /etc/vbox/networks.conf
* 0.0.0.0/0 ::/0
EOF
```


## Start and enter in guest VM

```sh
$ vagrant up
$ vagrant ssh
```

