# Vagrant WSL2 with VirtualBox

Simple example to up Apache server in VM

## Install

```sh
$ wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install vagrant
$ export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
$ export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
$ vagrant plugin install virtualbox_WSL2
$ vagrant --version
Vagrant 2.2.19
```

Cloning project to folder mount to Windows partition

## Prepare

```sh
# for example /mnt/c/opt
$ cd /mnt/c/opt/
$ git clone @
```

## Execution

```sh
$ vagrant up
```

## Troubleshooting

- Problem to connect SSH

```sh
$ cp /mnt/c/opt/vagrant/.vagrant/machines/default/virtualbox/private_key /opt/private_key
$ chmod 600 /opt/private_key
$ rm -rf /mnt/c/opt/vagrant/.vagrant/machines/default/virtualbox/private_key
$ sudo ln -s /opt/private_key /mnt/c/opt/vagrant/.vagrant/machines/default/virtualbox/private_key
$ vagrant ssh-config > ssh-vagrant
$ vagrant reload
```

## Refer

https://blog.thenets.org/how-to-run-vagrant-on-wsl-2/