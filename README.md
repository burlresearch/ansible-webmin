Server Provisioning with Ansible 
===

## Robots Building Robots


# Introduction

In my last article, [4](Webmin Configuration on CentOS), I discussed all the steps that I like to take when I setup a new server.
Not that I actually *like* taking all those steps, just that's what I typically want done.
Like any good programmer, I am actually very lazy, so there must be a better way do all of this.

And, of course, there is.
I'd like to take the time to introduce how we use a lovely tool called **Ansible** that will help us when it comes to performing all the steps that we need to do to build out a new server.
In fact, Ansible can be used for a whole lot more.

What I like about Ansible is that is does it's task in a relatively simple way.
Due to it's ease of use, it makes a great tool for doing everything that I talked about last time.

# Samples

This little bit is indented:

	while(true) {
		continue;
	}


This little bit is ticked:

```
while(true) {
	continue;
}
```

This little snippet is poked:

> let nothing you dismay

Betcha output is all different.

# Commands

	vagrant up
	vagrant ssh
		[vagrant@webmin ~]$ sudo passwd
		[vagrant@webmin ~]$ exit
	ssh-copy-id root@webmin.76labs.com
	pushd ~/src/ansible/webmin
	ansible-playbook -i hosts site.yml
	ansible-playbook -i hosts percona.yml

# TL;DR

In conclusion ...

---
[1]:http://wiki.centos.org/Manuals/ReleaseNotes/CentOS6.4 "CentOS 6.4"
[2]:http://www.virtualmin.com/documentation "VirtualMin"
[3]:http://www.webmin.com
[4]:http://76design.com/provision-webmin-centos
