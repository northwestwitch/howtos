## Setting up podman on macOS using VirtualBox and Vagrant

This howto is based on the following [article](https://medium.com/faun/avengers-of-container-world-episode-1-podman-hands-on-f81d8ee93b57) from Dec 2020.

1. Install VirtualBox from [this page](https://www.virtualbox.org/wiki/Downloads)
2. Install vagrant from [this page](https://www.vagrantup.com/docs/installation)
3. move to a directory where your repo is located
4. Initialize Vagrant with the command:
```
vagrant init centos/8
```

Note that a file with the following configuration will be created:
```
Vagrant.configure("2") do |config|
 config.vm.box = "centos/8"
end
```

5. Install the CentOS VM in the VirtualBox:
```
vagrant up
```
6. Check the virtual machine specifics (and that it's running) by executing `virtualBox`

7. Log in the CentOS with the command `vagrant ssh`. After that you'll be logged in the CentOS shell.

8. Install podman on CentOS:
```
sudo dnf -y module disable container-tools
sudo dnf -y install 'dnf-command(copr)'
sudo dnf -y copr enable rhcontainerbot/container-selinux
sudo curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo https://download.opensuse.org/repositories/devel:/kub ic:/libcontainers:/stable/CentOS_8/devel:kubic:libcontainers:stable.repo
sudo dnf -y install podman
sudo dnf -y update
```

9. Check podman version: `podman version`

10. Check podman info: `podman info`

11. Useful commands:
  - `podman ps`
  - `podman images`

12. Command to exit from the machine: `exit`
