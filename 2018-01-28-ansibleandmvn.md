---
layout: post
title:  "Ansible and Maven"
image: ''
date:   2017-01-28 00:00:00
tags:
- Ansible
- Maven
description: ''
categories:
- Ansible
- Maven
---

https://www.youtube.com/watch?v=SgxtxzQJM4w

## ANSIBLE Roles:

- puppet modules / chef - cookbooks / ansible - role

- Apache  - role for apache
	- whatever is required for apache to run will be in the role


## Components of a role (apache):

1. Defaults = data about the role /application. Default variables like the default port=80

2. Files = the static files (without modifications) which need to be sent to the machine

3. handlers = tasks which are based on actions like triggers (in case the httpd.conf file of apache - do a restart of apache)

4. meta = information about the role, Author supported platforms, etc dependencies

5. tasks = Core logic or code. installation package, copying files etc

6. templates = similiar to files except that template supports modifications (dynamic files) jinja2 - templating language

7. vars = both vars and Defaults stores values however variables stored under vars have higher priority and dificult to override


All folders have a main.yml the execution of these actions will run from the main.yml
in the tasks we add:


*/tasks/main.yml*
{% highlight yaml script %}
---
# tasks file for apache
include install.yml
include configure.yml
include service.yml
{% endhighlight %}

*/tasks/install.yml*
{% highlight yaml script %}
---
#install apache
- name: install apace
  yum:
  name: httpd
  state: latest
{% endhighlight %}

*/tasks/configure.yml*
{% highlight yaml script %}
---
#configuring httpd.conf send sample http file
- name: httpd.conf file (set this file in the /files folder)
  copy: src=httpd dest=/etc/httpd/conf/httpd.conf
  notify:
    - restart apache service

- name: send index.html
  copy: src=index.html dest=/var/www/html/index.html
{% endhighlight %}

*/tasks/service.yml*
{% highlight yaml script %}
---
#start apache service
- name: starting apache service
  service: name=httpd state=started
{% endhighlight %}

*/files/*
We need the files here that are mentioned in the other yml files.
(copy httpd.conf here)
cp /etc/httpd/conf/httpd.conf
Make your own index.html

*/handlers/main.yml*
{% highlight yaml script %}
---
# handler for files in apache
- name: restart apache service (this name must be the same as )
  service: name=httpd state=restarted
{% endhighlight %}


*/meta/main.yml*
{% highlight yaml script %}
---
Galaxy-info:
  author: Fons Drost
  Description: simple apache role
  Company: greater
  supported ? rhel7
{% endhighlight %}

Where you want have a overarching file to deploy and run the deploy to your servers


*/runner.yml*
{% highlight yaml script %}
---
- host: lsrv
  roles: apache
{% endhighlight %}

You can now run the playbook to initiate the roles to machines
