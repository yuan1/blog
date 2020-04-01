---
title: Scripts for turning Proxy server on/off
tags: Blog
categories:
  - Linux
toc: false
date: 2019-10-25 17:11:41
---

Scripts for turning Proxy server on/off::

1) /etc/environment contains only one line i.e. '$PATH:...'. And nothing else.

So! If you want to automate the process of turning proxy on and off without having to type allot. you can make two executable shell scripts proxyon.sh and proxyoff.sh as:

[proxyon.sh](http://gofile.me/3BPQ1/ZnpvWGA3E) :  

```bash

if [ $(id -u) -ne 0 ]; then
  echo "This script must be run as root";
  exit 1;
fi

if [ $# -eq 2 ]
  then

  grep PATH /etc/environment > lol.t;
  printf \
  "http_proxy=http://$1:$2/\n\
  https_proxy=http://$1:$2/\n\
  ftp_proxy=http://$1:$2/\n\
  no_proxy=\"localhost,127.0.0.1,localaddress,.localdomain.com\"\n\
  HTTP_PROXY=http://$1:$2/\n\
  HTTPS_PROXY=http://$1:$2/\n\
  FTP_PROXY=http://$1:$2/\n\
  NO_PROXY=\"localhost,127.0.0.1,localaddress,.localdomain.com\"\n" >> lol.t;

  cat lol.t > /etc/environment;


  printf \
  "Acquire::http::proxy \"http://$1:$2/\";\n\
  Acquire::ftp::proxy \"ftp://$1:$2/\";\n\
  Acquire::https::proxy \"https://$1:$2/\";\n" > /etc/apt/apt.conf.d/95proxies;

  rm -rf lol.t;

  else

  printf "Usage $0 <proxy_ip> <proxy_port>\n";

fi


```

[proxyoff.sh:](http://gofile.me/3BPQ1/zkocVRb1s):

```bash

if [ $(id -u) -ne 0 ]; then
  echo "This script must be run as root";
  exit 1;
fi

grep PATH /etc/environment > lol.t;
cat lol.t > /etc/environment;

rm -rf lol.t;

```

How to use: Once you have made these scripts, make them executable, you may keep them anywhere you like. To turn on proxy all you have to do is go to the directory containing the 'proxyon.sh' script and then you need to type sudo ./proxyon.sh {host} {port}. As an example consider this:

 $ sudo ./proxyon.sh 10.2.20.17 8080
 OR
 $ sudo ./proxyon.sh myproxy.server.com 8080
Where '10.2.20.17' is the proxy server's IP - you can also type something like myproxy.server.com - and '8080' is the port. After that just log out and login to your account, to make sure that everything is set. You can start using the internet or whatever then. And when you want to turn the proxy off, go to the directory containing 'proxyoff.sh' and type:

 $ sudo ./proxyoff.sh
This will unset all of your proxies. Now logout and login again to switch to normal mode.