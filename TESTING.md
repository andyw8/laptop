# Testing

Laptop is tested by using it to provision a fresh VM. The process is 
lengthy, scripted, and relies on Vagrant.

## Usage

1. Install [VirtualBox][]
2. Install [Vagrant][]
3. Execute `./test/runner.sh`

[VirtualBox]: https://www.virtualbox.org/
[Vagrant]: http://www.vagrantup.com/

## Process

Found at `test/Vagrantfile.*` is one Vagrantfile for each environment in 
which to test laptop. For each Vagrantfile found, the following occurs:

1. The file is symlinked to ./Vagrantfile
2. `vagrant destroy` is called to clean up any leftover VMs
3. `vagrant up` is called to initialize a new VM
4. If the Vagrantfile ends in `.mac` the mac script is run. Otherwise, 
   the linux-prerequisite and linux scripts are run
5. `vagrant halt` and `vagrant destroy` are called

## Assertions

In order for the test to pass, the following must all be true:

1. The VM is brought up successfully
2. The laptop script(s) run successfully
3. The VM reports its `$SHELL` as ZSH
4. The VM reports its ruby as 2.0.0p247.

## Open Issues

* Custom base box

Currently, Vagrant must install the `ubuntu-desktop` package before 
running laptop. This step could be done ahead of time and packaged into 
a custom base box used by the test.

* Additional Vagrantfiles

We'll need one for each supported distribution.

* Vagrantfile.mac

This will need to use the [VMware][] provider and means the test can 
only be run on an OSX host. The runner should be updated to skip this 
Vagrantfile when being run on a Linux host.

[VMware]: http://www.vmware.com/
