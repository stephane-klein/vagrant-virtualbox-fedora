# Install Vagrant + VirtualBox provider on Fedora

## Prepare your computer

Step1: disable secure boot.

```sh
$ sudo curl https://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -o /etc/yum.repos.d/virtualbox.repo 
$ sudo dnf install kernel-devel vagrant VirtualBox-6.1 -y
$ sudo /sbin/vboxconfig
$ vagrant --version
Vagrant 2.2.16
```

If you use Vagrant version < `2.2.18`, then you must execute:

```sh
cat <<EOF | sudo tee /etc/vbox/networks.conf

* 192.0.0.0/8
* 172.0.0.0/8
* 10.0.0.0/8
EOF
```

More information [here](https://github.com/Yohnah-org/Docker/issues/3#issuecomment-951118532).

## Start and enter in guest VM

```sh
$ vagrant up
$ vagrant ssh
```

