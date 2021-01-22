## Setting up podman on macOS using VirtualBox and Vagrant

This howto is based on the following [article](https://medium.com/faun/avengers-of-container-world-episode-1-podman-hands-on-f81d8ee93b57) from Dec 2020.

1. Install VirtualBox from [this page](https://www.virtualbox.org/wiki/Downloads)
2. Install vagrant from [this page](https://www.vagrantup.com/docs/installation)
3. Create a directory to store the VM files and move into it
4. Initialize Vagrant with the command:
```
vagrant init centos/8
```
A list of boxes available might be found here: https://app.vagrantup.com/boxes/search
Helpful [page](https://computingforgeeks.com/step-by-step-guide-on-using-existing-virtual-machines-with-vagrant/) explaining how to associate Vagrant to an existing VirtualBox :

Note that a file with the following configuration will be created:
```
Vagrant.configure("2") do |config|
 config.vm.box = "centos/8"
end
```

5. To be able to access the container from outside the host machine, modify this Vagrantfile by uncommenting the following line: `config.vm.network "public_network"`. To automatically select a bridged network on your computer you could add the network on the same line. For instance to use the wireless on my laptop I use the following configuration:
```
config.vm.network "public_network", bridge: [
      "en0: Wi-Fi (AirPort)",
]
```
If no bridge is selected, Vagrant will ask for a bridge while booting.

6. Install the CentOS VM in the VirtualBox:
```
vagrant up
```
7. Check the virtual machine specifics (and that it's running) by executing `virtualBox`

8. Log in the CentOS with the command `vagrant ssh`. After that you'll be logged in the CentOS shell.

9. Take a note on the inet ip displayed after running the command `inet a`: this will be the ip that can be accessed in the local network.

10. Install podman on CentOS 8:
```
sudo dnf -y module disable container-tools
sudo dnf -y install 'dnf-command(copr)'
sudo dnf -y copr enable rhcontainerbot/container-selinux
sudo curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/CentOS_8/devel:kubic:libcontainers:stable.repo
sudo dnf -y install podman
sudo dnf -y update
```

11. Check podman version: `podman version`

12. Check podman info: `podman info`

13. Useful commands:
  - `podman ps`
  - `podman images`

14. Command to exit from the machine: `exit`
