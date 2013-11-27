Server Provisioning with Ansible 
===
## Robots Building Robots
# Introduction

In my last article, [Webmin Configuration on CentOS][4], I discussed the steps setup a new server complete with [Webmin][3] and [Percona][0].
One glance at the article will make it obvious that there are quite a few steps.
Like any good programmer, I am very lazy, so there must be a better way to perform this automatically.

Of course, there is, using a process known as [server provisioning][7].
There are many different approaches that can be employed for doing this.
We have found [Ansible][8] to be one of the simplest and therefore, most appealing for our purposes.

# Ansible

The idea from the last article was basically writing down some of the modifications that we usually make when building a new server.
Roughly speaking, the overview of what we did from a new OS install can be listed:

- install webmin
- make sure Apache is installed
- install Percona (replacing MySQL)
- ensure PHP is up-to-date
- tweak the FastCGI configuration

Simple. But the article was *much longer* than that!
Wouldn't it be nice if we could just **script** the steps above and save that script so we could repeat, as needed?

That is precisely what Ansible does for us.

Some of the primary features of Ansible (and the ones that are important for us), are that it's:

1. streamlined and fast
1. requires no node agent installation
1. functions over SSH
1. built on Python

The basic idea with the Ansible approach is to build *playbooks*.
Simply enough, these playbooks contain *plays*, which are simply snippets that allow us to script the steps of the deployment tasks.

## Our First Playbook

Basically, in order to create our first playbook, we can literally just start scripting.
The following snippet will actually perform all the steps we need to do to install webmin on a fresh machine:

	---
	- hosts: all
	  user: root
	  tasks:
	  - name: ensure wget present
		yum: name=wget state=present
	  - name: download virtualmin install script
		shell: wget http://software.virtualmin.com/gpl/scripts/install.sh creates=/root/install.sh
	  - name: virtualmin install executable
		file: path=/root/install.sh mode=0755
	  - name: virtualmin install (possibly ~20 mins)
		shell: ~/install.sh --yes chdir=/root
	  - name: Virtualmin Post-Installation Wizard
		pause: prompt="virtualmin post-installation, https://{{ansible_hostname}}.76labs.com:10000"

Another of the attractive features of Ansible is the **declarative syntax** it uses.
I find the script above very readable and easy to follow. 


## More Advanced Layout

	.
	├── site.yml
	├── hosts
	└── roles
		├── iptables
		│   ├── handlers
		│   │   └── main.yml
		│   └── tasks
		│       └── main.yml
		├── percona
		│   ├── handlers
		│   │   └── main.yml
		│   └── tasks
		│       └── main.yml
		└── webmin
			└── tasks
				└── main.yml


# <span id="conclusion">TL;DR</a>

In conclusion ...

---
[1]:http://wiki.centos.org/Manuals/ReleaseNotes/CentOS6.4 "CentOS 6.4"
[2]:http://www.virtualmin.com/documentation "VirtualMin"
[3]:http://www.webmin.com "Webmin"
[4]:http://76design.com/provision-webmin-centos "Webmin Configuration on CentOS"
[5]:http://iweb.com/cloud "iWeb Cloud Services"
[6]:#conclusion
[7]:http://en.wikipedia.org/wiki/Provisioning#Server_provisioning
[8]:http://www.ansibleworks.com/tech/
