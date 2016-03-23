# Exploitation Training -- CVE-2013-2028: Nginx Stack Based Buffer Overflow

This repository contains the nginx 1.4.0 source code as well as precompiled binaries (with and without stack cookies).
There's also a Vagrantfile for easy setup.

Announcement and patch: http://mailman.nginx.org/pipermail/nginx-announce/2013/000112.html
Bug writeup: http://www.vnsecurity.net/research/2013/05/21/analysis-of-nginx-cve-2013-2028.html

## Setup

```bash
vagrant up
vagrant ssh
```

## Running

```bash
sudo /vagrant/bin/nginx1
```

Nginx is exposed on port 80 inside the VM on port 8080 outside (on the host).

```
# Inside VM
curl 127.0.0.1

# Outside VM
curl 127.0.0.1:8080
```

## Debugging

```bash
sudo gdb /vagrant/bin/nginx1
gdb> set follow-fork-mode child
gdb> r
```

## Obtaining/generating these files

You don't need to do this to develop your exploit, this is mostly just for the record.

#### Getting the source code

```bash
# Clone repository
hg clone http://hg.nginx.org/nginx
# See tags
hg tags
# Checkout 1.4.0
hg up 7809529022b8
```

#### Building
Without stack cookies:
```bash
./auto/configure --without-http_rewrite_module --without-http_gzip_module
vim objs/Makefile
# Add '-fno-stack-protector' to the CFLAGS
make -j4
sudo make install
```

With stack cookies:
```bash
./auto/configure --without-http_rewrite_module --without-http_gzip_module
make -j4
sudo make install
```

#### Running

```bash
# Webroot in /usr/local/nginx/html/
sudo ./objs/nginx
```
