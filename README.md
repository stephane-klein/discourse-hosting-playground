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
$ sudo -i
# cd /vagrant/
# docker-compose up -d
```

Go to http://forum.example.com to see Discourse page.  
Go to http://forum.example.com:1080 to see Maildev instance, to check the emails sent by Discourse.

## How I write docker-compose discourse service?

I used `./launcher start-cmd app`:

```
root@ubuntu2210:/var/discourse# ./launcher start-cmd app
x86_64 arch detected.
+ true run --shm-size=512m -d --restart=always -e LANG=en_US.UTF-8 -e RAILS_ENV=production -e UNICORN_WORKERS=4 -e UNICORN_SIDEKIQS=1 -e RUBY_GLOBAL_METHOD_CACHE_SIZE=131072 -e RUBY_GC_HEAP_GROWTH_MAX_SLOTS=40000 -e RUBY_GC_HEAP_INIT_SLOTS=400000 -e RUBY_GC_HEAP_OLDOBJECT_LIMIT_FACTOR=1.5 -e DISCOURSE_DB_SOCKET=/var/run/postgresql -e DISCOURSE_DB_HOST= -e DISCOURSE_DB_PORT= -e LC_ALL=en_US.UTF-8 -e LANGUAGE=en_US.UTF-8 -e DISCOURSE_HOSTNAME=forum.example.com -e DISCOURSE_DEVELOPER_EMAILS=me@example.com,you@example.com -e DISCOURSE_SMTP_ADDRESS=maildev -e DISCOURSE_SMTP_PORT=1025 -e DISCOURSE_SMTP_USER_NAME=user@example.com -e DISCOURSE_SMTP_PASSWORD=password -e DISCOURSE_SMTP_ENABLE_START_TLS=false -e DISCOURSE_SMTP_DOMAIN=forum.example.com -e DISCOURSE_NOTIFICATION_EMAIL=noreply@forum.example.com -h ubuntu2210-app -e DOCKER_HOST_IP=172.17.0.1 --name app -t -p 80:80 -v /var/discourse/shared/standalone:/shared -v /var/discourse/shared/standalone/log/var-log:/var/log --mac-address 02:2e:fc:5c:6a:03 local_discourse/app /sbin/boot
```


## How I reconstruct Docker image?

Rebuild `stephaneklein/discourse:3.1.0.beta3` Docker image:

```
$ vagrant ssh
$ sudo -i
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
