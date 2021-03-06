Nginx 1.4 for ZippyKid
======================

This set of files lets us build Nginx 1.4.X for our systems quickly. 

What's the difference?
=====================

At ZippyKid, we don't use the stock Nginx. We've added some modules for our use.

1. The Pagespeed module by the Google Pagepseed team https://github.com/pagespeed/ngx_pagespeed
1. The cache purge module https://github.com/FRiCKLE/ngx_cache_purge

Pre Reqs.
=========

You'll need a system running Ubuntu 12.04 or higher, anything prior to that should work, but
it's not been tested, and will not be supported by us. 

```
    sudo apt-get install devscripts build-essential autotools-dev debhelper git libpcre3-dev libssl-dev
    mkdir ~/src
    cd ~/src
    git clone git://github.com/FRiCKLE/ngx_cache_purge.git
    wget https://github.com/pagespeed/ngx_pagespeed/archive/release-1.6.29.5-beta.zip
    unzip release-1.6.29.5-beta.zip
    cd ngx_pagespeed-release-1.6.29.5-beta/ 
    wget https://dl.google.com/dl/page-speed/psol/1.6.29.5.tar.gz
    tar -xzvf 1.6.29.5.tar.gz
```


Building your own
=================

I'm not an expert in debian package management, so some steps here are probably
stupid. I don't know any better right now. 

1. Download latest version of nginx
```
	wget http://nginx.org/download/nginx-1.4.2.tar.gz
```

2. Rename the tarball to something debian wants to work with
```
    mv nginx-1.4.2.tar.gz nginx_1.4.2.orig.tar.gz
    tar zxf nginx_1.4.2.orig.tar.gz
    cd nginx-1.4.2/
```
3. Download this repository

```    
    git clone git@github.com:zippykid/nginx.git zippykid
    mv zippykid/debian debian
```
4. Make sure we know to work with the right version of nginx
```
    vim debian/changelog
```
Change the version string to apply to the version we're building

6. Build your package 
```
    debuild -us -uc
```
If this is the first time you patched the source, you'll see an error message,
this just means the package builder saw a difference between the original
source file, and what you're trying to build. You can tell dpkg that this
is a patch by doing the following
```
    dpkg-source --commit
```
You'll be asked to give the patch a name ```pagespeed``` is a good name .. 

Install
=======

If all of the above sounds like crazy talk to you, it does to me, you can just
download/wget the repository off our CDN, and do a dpkg -i 

Link for direct download: [[ http://f5c02e01f08d943e6009-d3c8ef7013f91d32e2e4b8caf6f33e0a.r10.cf2.rackcdn.com/nginx_1.4.1-1_amd64.deb ]]

These builds are working great for us, on Ubuntu 12.04 systems, and I'm only
going to support them on that for the time being.   

   
