## Haproxy compilied for Centos 7

### Install

* Download the latest haproxy version

```sh 
export HAPROXY_MAJOR=1.8
export HAPROXY_VERSION=1.8.14
wget -O haproxy.tar.gz \ 
"https://www.haproxy.org/download/${HAPROXY_MAJOR}/src/haproxy-${HAPROXY_VERSION}.tar.gz" 
```



* Install pre packages

```sh
yum install -y inotify-tools wget tar gzip make gcc perl pcre-devel zlib-devel iptables \
openssl openssl-devel openssl-libs systemd-devel
```

* Compiling

```sh
tar xvfz haproxy.tar.gz
cd haproxy-1.8.14/
make TARGET=linux2628 USE_GETADDRINFO=1 USE_ZLIB=1 USE_REGPARM=1 USE_OPENSSL=1 \
USE_SYSTEMD=1 USE_PCRE=1 USE_PCRE_JIT=1 USE_NS=1
make install
``` 

* Install

```
install -d "/usr/sbin"
install -m 755 haproxy  "/usr/local/sbin"
install -d "/usr/share/man"/man1
install -m 644 man/haproxy.1 "/usr/local/share/man"/man1
```

### Options used to compile

```
[root@7aeb6f9453e4 haproxy-1.8.14]# ./haproxy -vv
HA-Proxy version 1.8.14-52e4d43 2018/09/20
Copyright 2000-2018 Willy Tarreau <willy@haproxy.org>

Build options :
  TARGET  = linux2628
  CPU     = generic
  CC      = gcc
  CFLAGS  = -O2 -g -fno-strict-aliasing -Wdeclaration-after-statement -fwrapv -fno-strict-overflow -Wno-unused-label
  OPTIONS = USE_GETADDRINFO=1 USE_ZLIB=1 USE_REGPARM=1 USE_OPENSSL=1 USE_SYSTEMD=1 USE_PCRE=1 USE_PCRE_JIT=1 USE_NS=1

Default settings :
  maxconn = 2000, bufsize = 16384, maxrewrite = 1024, maxpollevents = 200

Built with OpenSSL version : OpenSSL 1.0.2k-fips  26 Jan 2017
Running on OpenSSL version : OpenSSL 1.0.2k-fips  26 Jan 2017
OpenSSL library supports TLS extensions : yes
OpenSSL library supports SNI : yes
OpenSSL library supports : SSLv3 TLSv1.0 TLSv1.1 TLSv1.2
Built with transparent proxy support using: IP_TRANSPARENT IPV6_TRANSPARENT IP_FREEBIND
Encrypted password support via crypt(3): yes
Built with multi-threading support.
Built with PCRE version : 8.32 2012-11-30
Running on PCRE version : 8.32 2012-11-30
PCRE library supports JIT : yes
Built with zlib version : 1.2.7
Running on zlib version : 1.2.7
Compression algorithms supported : identity("identity"), deflate("deflate"), raw-deflate("deflate"), gzip("gzip")
Built with network namespace support.

Available polling systems :
      epoll : pref=300,  test result OK
       poll : pref=200,  test result OK
     select : pref=150,  test result OK
Total: 3 (3 usable), will use epoll.

Available filters :
        [SPOE] spoe
        [COMP] compression
        [TRACE] trace
```

### Author

Juan Enciso <juan.enciso@gmail.com>
