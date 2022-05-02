# Vagrant
This repo is home to vagrant config files relevant to UnumID. 

## First Time Use

1) Install [Vagrant](https://www.vagrantup.com/downloads). I would recommend installing with brew if possible.

```
brew install vagrant
```

If you don't have brew, install it as described [here](https://brew.sh) using:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Ensure is properly installed on your path by typing `vagrant` in the cli and should get command help.


2) Install VirtualBox. This [guide](https://cs.hofstra.edu/docs/pages/guides/vbox_mac.html) is fairly concise. Be sure to do the system security step. Otherwise will get [errors](https://www.howtogeek.com/658047/how-to-fix-virtualboxs-%E2%80%9Ckernel-driver-not-installed-rc-1908-error/).


## How to Use
After having Vagrant and VirtualBox installed 

1) Clone this repo.

2) Go to the directory of the box you would like to use. For example:

```
cd windows11
```

3) Run `vagrant up`.

First time the command will take some time as it needs to download the "box" with the os image. However after the first time this will be much quicker.

That's it. You now have a VM in VirtualBox as defined by the Vagrantfile up and running. The default user credentials are: 

username: `vagrant` 
password: `vagrant`


## Useful Vagrant Commands

- `vagrant up` - to start the vm
- `vagrant halt` - to stop the vm (power down)
- `vagrant suspend` - to save state and stop machine
- `vagrant snapshot` - to manage vm snapshots
- `vagrant ssh` - to ssh on to the machine. Default user (u: vagrant, pw: vagrant)

More info on Vagrant commands can be obtained by simply entering `vagrant` into the CLI.

## Sharing Files from Host to VM
Vagrant by default sets up the directory you ran `vagrant up` in as a shared volume on the guest OS. So any files you put in the `windows11`, for example, are automatically shared with the VM on the vm's user's path. The exact path is actually part of the `up` output. You can find it by looking for `Mounting shared folders...`

### Vagrant scp plugin
Alternatively one can use the vagrant scp plugin. It can be installed by 
```
vagrant plugin install vagrant-scp
```
Once installed one can scp files. This [guide](https://medium.com/@smartsplash/using-scp-and-vagrant-scp-in-virtualbox-to-copy-from-guest-vm-to-host-os-and-vice-versa-9d2c828b6197#:~:text=Method%20%23%202%3A-,sending%20file%20from%20Host%20OS%20to%20Guest%20VM%20using%20scp,-This%20is%20easy) maybe helpful in addition to the vagrant-scp [docs](https://github.com/invernizzi/vagrant-scp).

If you have just a single Vagrant guest, you can copy files over like this:

    vagrant scp <some_local_file_or_dir> <somewhere_on_the_vm>

If you have multiple VMs, you can specify it.

    vagrant scp <some_local_file_or_dir> [vm_name]:<somewhere_on_the_vm>

Copying files out of the guest works in the same fashion

    vagrant scp [vm_name]:<somewhere_on_the_vm> <some_local_file_or_dir>

If source is a directory it will be copied recursively.


#### Examples

If you have just one guest, you can copy files to it like this:

    vagrant scp file_on_host.txt :file_on_vm.txt

And from the guest like this:

    vagrant scp :file_on_vm.txt file_on_host.txt

Concretely something like:
```
vagrant scp testFile default:/Users/vagrant/testFile
```

## Troubleshooting
If getting an error first ensure you have enabled your security settings so code execution from Oracle is allowed [[1]](https://www.howtogeek.com/658047/how-to-fix-virtualboxs-%E2%80%9Ckernel-driver-not-installed-rc-1908-error/).

If still getting an error while unpacking a box then it is very likely an Disk Space usage. Please ensure you have at least 20GBs free per VM. Windows requires 14GB minimum just to start.
