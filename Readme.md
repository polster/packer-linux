Linux Boxes
===========

## Motivation

Automate and simplify the creation of Linux VMs (aka boxes) featuring a minimal setup to be the basis for various purposes.

## Requirements

* OS: Tested on OS X 10.11, may also work on other systems
* Tooling: Vagrant, Packer
* Virtualization provider: VMWare Fusion with Vagrant VMWare Plugin (needs an extra plugin license) or Virtualbox

## Basic usage

* Cd into the Linux version folder of choice and run (will build a Vagrant box based on Virtualbox):
```
make build
```
* Run the following command in order to create the box for a specific provider (e.g. VMWare):
```
make build PROVIDER=vmware
```
* Run the smoke test (Adds the box as VM, boots the VM, tries to connect via SSH, shuts the VM down and destroys the same):
```
make test PROVIDER=vmware
```

## Project structure

```
packer-linux
|- common
|   |- scripts        # common scripts
|   `- Makefile       # Command definition
|
|- linux-distro
|   `- scripts        # Linux distro specific scripts
|
`- linux-distro-version
    |- ks.cfg         # Kickstart configuration
    |- Makefile       # Symlink
    |- template.json  # Packer template
    `- Vagrantfile    # Vagrant config

```

## Security concerns

* The Linux boxes being created with the help of this project must be seen as development boxes without proper hardening
* For instance, the default user being created and used for the provisioning tasks has unrestricted sudo (which is far away from production)
* In case these boxes will be used in production a proper hardening will be a must
