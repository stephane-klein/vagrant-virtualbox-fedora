# Install Vagrant + VirtualBox provider + vagrant-hostmanager on Fedora Workstation

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
$ vagrant plugin install vagrant-hostmanager --plugin-version 1.8.9
```


```sh
$ vagrant --version
Vagrant 2.3.4
```

```sh
$ VBoxManage --version
7.0.8_rpmfusionr156879
```

```sh
$ cat <<EOF > /etc/vbox/networks.conf
* 192.0.0.0/8
* 172.0.0.0/8
* 10.0.0.0/8
EOF
```


## Start and enter in guest VM

```sh
$ vagrant box update  # can fix some issue, like https://github.com/stephane-klein/vagrant-virtualbox-fedora/issues/1
$ vagrant up
$ vagrant ssh
vagrant@foobar:~$ ping -c1 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=63 time=15.8 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 15.800/15.800/15.800/0.000 ms
```

Install nginx http server:

```sh
$ sudo -i
# apt install nginx
```

Test curl to access to http server from host:

```sh
$ curl http://foobar
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

```sh
$ curl http://foobar.example.com
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
