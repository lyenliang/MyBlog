title: Installing nginx from source on Ubuntu 14.04
author: lyenliang
date: 2017-04-28 17:26:56
tags:
---
These installation steps are just for my reference. Visit [INSTALLING NGINX OPEN SOURCE](https://www.nginx.com/resources/admin-guide/installing-nginx-open-source/) if you need a more detailed installation guide.

    sudo apt-get update
    sudo apt-get install build-essential

Next, go to [nginx source releases]( https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#source-releases) and find the download link.  
In my case it is `http://nginx.org/download/nginx-1.10.1.tar.gz?_ga=1.4610931.1556411009.1493370198`. Download it with `wget`:

    wget http://nginx.org/download/nginx-1.10.1.tar.gz?_ga=1.4610931.1556411009.1493370198
    
Extract the downloaded file:

    tar -zxvf nginx-1.10.1.tar.gz?_ga=1.4610931.1556411009.1493370198
 
 Switch to nginx's directory.
 
    cd nginx-1.10.1/
    
Install libraries for nginx:
   
    sudo apt-get install libpcre3 libpcre3-dev libpcrecpp0 libssl-dev zlib1g-dev
    
The [PCRE](http://pcre.org/) (libpcre3, libpcre3-dev, and libpcrecpp0 ) library provides support for regular expression.

The [zlib](http://www.zlib.net/) library is used for headers compression.

The [OpenSSL](https://www.openssl.org/) library is used for supporting HTTPS protocol.

Configure the modules you want to install with [Installation and Compile-Time Options](https://www.nginx.com/resources/wiki/start/topics/tutorials/installoptions/)
    
    ./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-debug --with-pcre --with-http_ssl_module 
    make
    sudo make install