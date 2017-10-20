---
layout: post
title: "Bash Scripting"
date: 2017-10-05 15:00:00
image: ''
description: 'bash scripting'
tags:
- bash
- scripting
- opperators
- redirects
- io
categories:
- bash
---
<img src="http://www.unixstickers.com/image/cache/data/stickers/binbash/Bash-new.sh-600x600.png" width="50%" height="50%">

# Bash Scripting

Like in math bash can perform comamnds like (1+2)-3=0
This is done with an Expression that looks like this [[ 1 + 1 ]]

## Opperators
{% highlight javascript %}
	"A ; B" 	Run A and then B regardless of success of A
	"A && B" 	Run B if A succeeded
	"A || B" 	Run B if A failed
	"A &" 		Run A in background
{% endhighlight %}

## Redirecting Output
You can redirect Input/Output
{% highlight javascript %}
	1 > 1	Redirect to a file and overwrite
	1 >> 1	Redirect to a file and append at bottom
	2>&1 	Redirects Channel 2 (Standard Error) and Channel 1 (Standard Output) to the same place which in this context is Channel 1 (Standard Output), and thence your log file.
{% endhighlight %}

## Combining the topics! Using the `||` operator with -x
{% highlight javascript %}
	[root@qmlf666 ~]# [[ -x /bin/ping ]] || ping 8.8.8.8
	[root@qmlf666 ~]# [[ -x /bin/pingwrong ]] || ping 8.8.8.8
	PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
		64 bytes from 8.8.8.8: icmp_seq=1 ttl=56 time=1.39 ms
		64 bytes from 8.8.8.8: icmp_seq=2 ttl=56 time=1.12 ms
		64 bytes from 8.8.8.8: icmp_seq=3 ttl=56 time=1.21 ms
		64 bytes from 8.8.8.8: icmp_seq=4 ttl=56 time=1.19 ms
		--- 8.8.8.8 ping statistics ---
	6 packets transmitted, 6 received, 0% packet loss, time 5006ms
	rtt min/avg/max/mdev = 1.105/1.196/1.394/0.104 ms
{% endhighlight %}

What this does is ( -x ) this checks if the file ( /bin/ping ) is present and returns a TRUE or FALSE
This results in the following:

**[[ -x /bin/ping ]] `||` ping 8.8.8.8**

Because that part is in a expression is handled first the statement run at the end is:

**true `||` ping 8.8.8.8**

The opperator `||` says that if the left side of the opperator is true it will not run the right side so the ping does not run because /bin/ping exists.

With the following command:

**[[ -x /bin/pingwrong ]] `||` ping 8.8.8.8**

So this becomes:

**false `||` ping 8.8.8.8**

The ping will run because the left side is false so the `||` will run the right command.

## Sources
1. <a href="http://www.tldp.org/LDP/abs/html/io-redirection.html" target="_blank">Bash I/O Redirectors</a>
2. <a href="http://tldp.org/LDP/abs/html/ops.html" target="_blank">Bash all simple Opperators</a>
3. <a href="http://tldp.org/LDP/abs/html/comparison-ops.html" target="_blank">Bash Comparison Opperators</a>
