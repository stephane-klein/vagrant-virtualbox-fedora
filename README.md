# Install Vagrant + VirtualBox provider on Fedora

## Prepare your computer

Step1: disable secure boot.

```sh
$ sudo curl https://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -o /etc/yum.repos.d/virtualbox.repo 
$ sudo dnf install kernel-devel vagrant VirtualBox-6.1 -y
$ sudo /sbin/vboxconfig
```

## Start and enter in guest VM

```sh
$ vagrant up
$ vagrant ssh
```

