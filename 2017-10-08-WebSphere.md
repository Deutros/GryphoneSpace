---
layout: post
title:  "WebSphere"
image: ''
date:   2017-10-08 00:00:00
tags:
- WebSphere
description: ''
categories:
- WebSphere
- Java
---

<img src="https://cdn.xebialabs.com/assets/files/plugins/websphere-application-server.jpg" width="50%" height="50%">

## Server

{% highlight bash script %}
##############################
# WebApplication             #
# Cell or profile 	         #
# **************************##
# *Node 1       | Node 2    *#
# * ------------	          *#
# *|  instance. |	          *#
# * ------------            *#
# ***************************#
# httpd                      #
##############################
{% endhighlight %}

Linux Server with on it a webbaplication running a cell/profile with in that a node and the application for example ast01srv5594
A Cell can have multiple Nodes on one server unless you have the expensive package then you can have multiple nodes in a cell on multiple servers.

Server also runs an HTTPD apache server

{% highlight bash script %}
the webapplication server is at:
/opt/was85/as/profiles/nodet01/[bin/etc/log] and such
       |    |      |      |          |
       ▼    |      |      |          |
Websphere   ▼      |      |          |
Application Server ▼      |          |
       Profile / Class    ▼          |
     	                 Node        ▼      
                            Application
{% endhighlight %}


The webapplication server can be reached on
`https://server.x.nl:5003/admin`


## Websphere WebInterface
DataSource 	= Database
JBDC	   	= Java Database Connection
JMS	 	= Java Messaging System
QSSC		= de queue manager waar we naar toe sturen

MQ = de message queue van IBM deze kan ook JMS (Java Message System)
IBM WebSphere Transactie Log stuur dus zijn berichten naar MQ

Wij gebruiken Base WEbsphere Package/Versie

The message Logs Location:
`/opt/was85/as/profiles/nodet01/translog/cellt01/nodet01/(instance)/(logs)`

voor verbinding is nodig
host
node verbinding
poort
queue coonnection factory

Server with RHEL7
Websphere Application java hosting PEGA inside (websphere does all the connections to other sources)
HTTPD Application apache


## Queue Information
### What is queue connection factory in WebSphere?
WebSphere MQ messaging provider queue connection factory settings. ... These configuration properties control how connections are created to associated JMS queue destinations. A WebSphere MQ queue connection factory is used to create JMS connections to queues provided by WebSphere MQ for point-to-point messaging.


### WebSphere MQ queues
A queue is a container for messages. Business applications that are connected to the queue manager that hosts the queue can retrieve messages from the queue or can put messages on the queue.

### QueuueConnectionFactory
A client uses a QueueConnectionFactory object to create QueueConnection objects with a point-to-point JMS provider. QueueConnectionFactory can be used to create a QueueConnection , from which specialized queue-related objects can be created.


A WebSphere MQ topic connection factory is used to create JMS connections to topic destinations provided by WebSphere MQ for publish/subscribe messaging. ... In the navigation pane, click Resources > JMS->Topic connection factories to display existing topic connection factories.
