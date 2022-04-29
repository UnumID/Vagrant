# Vagrant
This repo is home to vagrant config files relevant to UnumID. 

## First Time Use

1) Install [Vagrant](https://www.vagrantup.com/downloads). I would recommend installing with brew if possible.

```
brew install vagrant
```

Ensure is properly installed on your path by typing `vagrant` in the cli and should get command help.


2) Install VirtualBox. This [guide](https://cs.hofstra.edu/docs/pages/guides/vbox_mac.html) is fairly concise. Be sure to do the system security step. Otherwise will get [errors](https://www.howtogeek.com/658047/how-to-fix-virtualboxs-%E2%80%9Ckernel-driver-not-installed-rc-1908-error/).


## How to Use
After having Vagrant and VirtualBox installed 

1) Go to the director of the box you would like to use.

2) Run `vagrant up`.

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

## Troubleshooting
If getting an error first ensure you have enabled your security settings so code execution from Oracle is allowed [[1]](https://www.howtogeek.com/658047/how-to-fix-virtualboxs-%E2%80%9Ckernel-driver-not-installed-rc-1908-error/).

If still getting an error while unpacking a box then it is very likely an Disk Space usage. Please ensure you have at least 20GBs free per VM. Windows requires 14GB minimum just to start.
