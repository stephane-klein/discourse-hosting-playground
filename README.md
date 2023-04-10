# Discourse hosting playground

This project is in work in progress.  
There is a high chance that you will get an error if you follow the instructions in this readme.

Repository starting point issue (in French): https://github.com/stephane-klein/backlog/issues/191

This repository contains a environment that allows to test [Discourse](https://github.com/discourse/discourse) deployment.

My documentation entry point: [How Do I Install Discourse?](https://github.com/discourse/discourse/blob/main/docs/INSTALL.md)

If you want to install and configure Vagrant and Virtualbox on Fedora Workstation, you can check this repository: https://github.com/stephane-klein/vagrant-virtualbox-fedora


```sh
$ vagrant plugin install vagrant-hostmanager --plugin-version 1.8.9
```

```sh
$ vagrant up
```

```
$ vagrant ssh
$ sudo su
# cd /vagrant/
# docker-compose up -d
```

Go to http://forum.example.com to see Discourse page.  
Go to http://forum.example.com:1080 to see Maildev instance, to check the emails sent by Discourse.


## How I reconstruct Docker image?

Rebuild `stephaneklein/discourse:3.1.0.beta3` Docker image:

```
# git clone https://github.com/discourse/discourse_docker.git /var/discourse
# cd /var/discourse
# git checkout 7a7c47eefaf2d9a2b573f42e7bfb31bfe7402250 
# cp /vagrant/app.yml containers/app.yml
# ./launcher bootstrap app
# docker images | grep "local_"
local_discourse/app       latest              57659bb1bc11   3 hours ago     3.98GB
# docker tag local_discourse/app stephaneklein/discourse:3.1.0.beta3
# docker push stephaneklein/discourse:3.1.0.beta3
```
