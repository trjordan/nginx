Nginx 1.3 for ZippyKid
======================

This set of files lets us build Nginx 1.3.X for our systems quickly. 

What's the difference?
=====================

We use the SPDY patch, the Nginx Cache purge module, and sometimes the pagespeed modules 

Building your own
=================

I'm not an expert in debian package management, so some steps here are probaly
stupid. I don't know any better right now. 

1. Download latest version of nginx
```
	wget http://nginx.org/download/nginx-1.3.14.tar.gz
```

2. Rename the tarball to something debian wants to work with

    mv nginx-1.3.14.tar.gz ngginx_1.3.14.orig.tar.gz

3. Download this repository
    
    git clone git@github.com:zippykid/nginx.git
    mv nginx/debian debian

4. Make sure we know to work with the right version of nginx

    vim debian/changelog
Change the version string to apply to the version we're building

5. Download the SPDY patch and patch the source. 
    
    wget http://nginx.org/patches/spdy/patch.spdy.txt
    patch -p1 < patch.spdy.txt

6. Build your package 

    debuild -us -uc
If this is the first time you patched the source, you'll see an error message,
this just means the package builder saw a difference between the original
source file, and what you're trying to build. You can tell dpkg that this
is a patch by doing the following

    dpkg-source --commit

You'll be asked to give the patch a name ```spdy``` is a good name .. 

Install
=======

If all of the above sounds like crazy talk to you, it does to me, you can just
download/wget the repository off our CDN, and do a dpkg -i 

Link for direct download: https://532fc975870e3f7ac694-d3c8ef7013f91d32e2e4b8caf6f33e0a.ssl.cf2.rackcdn.com/nginx_1.3.14-1_amd64.deb

These builds are working great for us, on Ubuntu 12.04 systems, and I'm only
going to support them on that for the time being.   

   
