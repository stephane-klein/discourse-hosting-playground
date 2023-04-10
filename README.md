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
$ sduo su
# /vagrant/
# git clone https://github.com/discourse/discourse_docker.git /var/discourse
# cd /var/discourse
# git checkout 7a7c47eefaf2d9a2b573f42e7bfb31bfe7402250 
# cp /vagrant/app.yml containers/app.yml
```
