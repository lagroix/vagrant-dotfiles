# Vagrant Dotfiles

Configuration management solution used to automate the installation/customization of my SRE workstation host and virtual machine environment. This has been tested to work with both Ubuntu Linux (19.10) and Mac OS X (10.14.X) host workstations.

## Backstory

The purpose of this repository is as follows: I want to keep my host operating system and my SRE workstation virtual machine separate and distinct. I want to do ALL of my command-line work from a full blown, LTE, Ubuntu Linux workspace and I want to be able to run graphical tools, such as a web browser or IDE from the host workspace. And I don't want either one to contaminate the other. (Mostly, I don't EVER want to install `npm` on my host operating system because good luck with managing all that mess... and I want to use REAL GNU core utility programs -- not the substandard Mac Os versions.)

Anyhow, the theory behind my solution is sound. Give me a:

- MacBook
- Linux Workstation (Ubuntu/Debian only)
- Windows Desktop (**TODO**)

and I should have no trouble configuring the machine to do 100% of my job in a 100% consistent environment. For example, if we are running Ubuntu 18.04 in the cloud, then I want to be able to code in Ubuntu 18.04 and, for the sake of performance, I shouldn't be forced to run my graphical applications from inside the VM. Yes, you could probably do all of this by linking together various containers. But I don't want to run Mac's or Window's version of docker anyway. I want to run docker in Linux. And I am old and comfortable with VMs and both Vagrant and VirtualBox are available for every platform and performance (VirtualBox, I am looking at you) is NOT an issue because, like I said, I still live, for the most part, in the native desktop environment.

All that being said, in the end, I basically have the following:

- A bootstrap script that automates most of the configuration required to set up the host machine to run the virtual machine.

- Another bootstrap script that automates all of the configuration required to set up my SRE workstation in the VM.

- And a reliable method (`ssh_vm`) to blindly SSH to the VM in order to gain immediate access to all of my standardized command-line tools, utilities, cloud credentials, and various Python and Golang programming platforms.

## Requirements

To configure your host computer and provision the virtual machine, you will need to install a small number of required applications.

For Ubuntu/Debian Linux:

- sudo access
- git
- make

If you are running Mac OS X, then you will also require:

- homebrew

## Quickstart

To kick everything off, first clone this repository to the root of your home directory.

```
cd 
git clone https://github.com/strongbrent/vagrant-dotfiles.git
```

Then navigate to the project directory.

```
cd vagrant-dotfile
```

To install the host computer's requirements, run the following:

```
make host
```

WARNING! You will be prompted to continue... you will also be warned that you are ABOUT TO INSTALL SOFTWARE AND OVERWRITE FILES IN YOUR HOME DIRECTORY (and other locations...). Proceed at your discretion.

To provision the virtual machine, run the following:

```
make vm
```

And to install the `ssh_vm` script to your `${HOME}\bin` directory, run this command:

```
make bin
```

After that, since `${HOME}\bin` is now in your PATH, you can run the following command from anywhere to SSH to your VM:

```
ssh_vm
```