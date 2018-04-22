---
layout: post
title: Remote SSH on home computer
meta: Setting up remote ssh on home computer
category: ssh
---

# Setting up a Remote SSH server on a Home Computer

![SSH](https://cdn-images-1.medium.com/max/800/1*ulHC0mFaAxK9TxpXuFHtIg.png)

I have recently set up my [Deep Learning
box](http://sritanu.github.io/deeplearning/2018/04/22/Deep-Learning-Box-Setup-and-Installation.html). We will be discussing about setting up a remote ssh server on the home
computer so that we can log in to our desktop from other machines(laptops in my case).

I will be keeping the post short as there are a plethora of articles (for [example](https://www.ssh.com/ssh/)) that discusses about ssh in depth. Let’s dive straight in.

SSH or Secure Shell is a secure protocol to log into remote systems.

Now, the client-machine(laptop) will try to connect remotely to the server-machine(desktop).

> SSH has primarily two components (sys-admins don’t go crazy on me here):
> 1. ssh : The command that allows us to log into servers from the client
> 2. sshd : ssh daemon that runs on the server which allows other clients to connect to
the server.

ssh is enabled when you install a fresh Ubuntu OS. But the sshd isn’t. You can do few checks **on your server(desktop)** now to see if this is the case.

Run `which ssh` and you will get an output where your ssh is but you won’t be
getting any when you run `which sshd`:
```
$ which ssh
/usr/bin/ssh
$ which sshd
$
```
Do another check now. Trying logging into your localhost from the desktop. Run `ssh 127.0.0.1` and your connection will be refused.
```
$ ssh 127.0.0.1
ssh: connect to host 127.0.0.1 port 22: Connection refused
```
To start ssh deamon you need to install ssh. Run :
```
$ sudo apt-get install ssh
```
Now, try running `which ssh` and `which sshd` . You should be getting their outputs now.
```
$ which ssh
/usr/bin/ssh
$ which sshd
/usr/sbin/sshd
```
Now, before doing anything else, **generate** your SSH-key as mentioned [here](https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html).

You can now connect to `ssh 127.0.0.1`.

We need to get the IP address of the server machine so that we can login remotely from the client. Run `$ ifconfig | grep "inet addr"` on your terminal and note down the IP address.

Go to your **client machine**, fire up the terminal and check if you can ping your server machine:
```
$ ping -c3 <ip_address_of_server>
```
Hopefully you can. Now run:
```
$ ssh <username_of_your_server>@<ip_address_of_server>
```
It will prompt you to enter `yes\no` to continue connecting to the server. Accept it.

Enter the password with which you login to your server. And you can see a welcome message on your terminal with your server’s command prompt.

To exit just type `exit`, hit enter and you are back to your client’s command prompt.

Bingo!! You have successfully logged in to your server from your client.

**Update** : Slav Ivanov has done a great work in describing how to work on Jupyter notebook via ssh port forwarding. You can check out the **Jupyter Notebook** section
[here](https://blog.slavv.com/the-1700-great-deep-learning-box-assembly-setup-and-benchmarks-148c5ebe6415).
