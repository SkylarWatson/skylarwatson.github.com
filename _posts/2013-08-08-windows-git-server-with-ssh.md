---
layout: post
title: "Setting up a Windows Git Server using SSH"
description: ""
category: 
tags: [git]
---
In this article we will install Git on our client and server, setup SSH, push our project to our server, and finally allow our client(s) to clone our repository. For the purpose of the scripts below; I've installed Git in C:\Git and CopSSH in C:\ICW.

Install <a href="https://code.google.com/p/msysgit/downloads/list">Git</a> (msysgit) on client server

Install <a href="https://www.itefix.no/i2/copssh-get?quicktabs_6=1#quicktabs-6">CopSSH</a> on server

After it's installed, and you've activated a user through CopSSH's control panel we'll then need to add Git to our PATH. This will allow us to execute remote Git commands through SSH. To do this you can open a unix bash shell which came as part of CopSSH and execute the following:

```bash
 cd /cygdrive/c/ICW/home/username
 echo -e "export PATH=\$PATH:/cygdrive/c/Git/bin" >> .bashrc
 echo -e "export PATH=\$PATH:/cygdrive/c/Git/libexec/git-core" >> .bashrc
```

To verify the script above worked properly you can open a terminal window on the client machine and simply try to SSH into the box. (Note: you will be prompt for the users password)

```bash
	ssh user@192.168.0.1
```

Now that were on the server you should be able to execute any Git command. To test this were going to print the version of Git we have installed by running the following command:

```bash
	git --version
```

<li>Generate keys</li>

We've now verified that we can SSH into our server and execute Git. Next, were going to generate our public and private keys. This will be done on the client machine and the public key will be transferred to the server.
	
```bash
	cd C:/Users/username
	mkdir .ssh
	ssh-keygen -t rsa -N '' -f .ssh/id_rsa
	scp .ssh/id_rsa.pub user@server:.ssh/authorized_keys
```

Our keys have now been generated and a copy of our public key now resides in a file on our server named authorized_keys. Each line in this file corresponds to a public key. We should now be able to SSH to our server without being prompt for the password.
	
```bash
	ssh user@192.168.0.1
```

<li>Getting our repository on the server</li>

To get our project onto the server we'll first need to clone it. Once we have our clone we just need to get it to our server. The commands for these steps can found below.</br></br>

```bash
	git clone --bare project project.git
	scp -r project.git user@server:"C:/path/to/repo/project.git"
```

Now your client machine should be able to clone your repository located on your server by issuing the following command:

```bash
	git clone user@server:"C:/path/to/repo/project.git"
```