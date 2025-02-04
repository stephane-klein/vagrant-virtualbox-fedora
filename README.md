# Install Vagrant + VirtualBox provider on Fedora Workstation

Host: Fedora Workstation 41  
Guest: [Ubuntu 24.04 LTS](https://en.wikipedia.org/wiki/Ubuntu_version_history#Ubuntu_24.04_LTS_(Noble_Numbat))

[VirtualBox](https://en.wikipedia.org/wiki/VirtualBox) package is installed from [RPM Fusion](https://rpmfusion.org) repository.

## Prepare your computer

1. disable secure boot.
2. Configure RPM Fusion (if you haven't already):

```sh
$ sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

3. Install VirtualBox package

```sh
$ sudo dnf install -y VirtualBox
```

4. Configure Hashicorp RPM repository to install Vagrant (if you haven't already):

```sh
$ sudo dnf install -y dnf-plugins-core
$ sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/fedora/hashicorp.repo
```

5. Install Vagrant:

```sh
$ sudo dnf -y install vagrant
```

6. Checking installed versions:

```sh
$ vagrant version
Installed Version: 2.4.1
Latest Version: 2.4.1
```

```sh
$ VBoxManage --version
7.0.16_rpmfusionr162802
```

At the time of writing, Vagrant is not compatible with the latest version of Virtualbox: <https://github.com/hashicorp/vagrant/issues/13501>.

```sh
$ cat <<EOF > /etc/vbox/networks.conf
* 192.0.0.0/8
* 172.0.0.0/8
* 10.0.0.0/8
EOF
```

## Vagrant Ubuntu image

Since version 24.04, Ubuntu [no longer seems to offer the official Vagrant image](https://discourse.ubuntu.com/t/ubuntu-24-04-lts-noble-numbat-release-notes/39890):

> Starting in Ubuntu 24.04, Ubuntu no longer produces Vagrant images. Documentation regarding creating an Ubuntu Base Image from scratch is provided at https://documentation.ubuntu.com/public-images/en/latest/public-images-how-to/build-vagrant-with-bartender/ 84.

I've chosen more or less arbitrarily to use the following Vagrant image: [`bento/ubuntu-24.04`](https://portal.cloud.hashicorp.com/vagrant/discover/bento/ubuntu-24.04)

If you know of a reliable image, please feel free to share it with me <contact@stephane-klein.info>.

## Start and enter in guest VM

```sh
$ vagrant box update  # can fix some issue, like https://github.com/stephane-klein/vagrant-virtualbox-fedora/issues/1
$ vagrant up
$ vagrant ssh
```

