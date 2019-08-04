

---

let's add some ssl now...

Confirm openssl is installed  `sudo apt show openssl`

>     ubuntu@ip-10-1-1-4:/var/www$ sudo apt show openssl
>     Package: openssl
>     Version: 1.1.1-1ubuntu2.1~18.04.4
>     Priority: important
>     Section: utils
>     Origin: Ubuntu
>     Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
>     Original-Maintainer: Debian OpenSSL Team <pkg-openssl-devel@lists.alioth.debian.org>
>     Bugs: https://bugs.launchpad.net/ubuntu/+filebug
>     Installed-Size: 1252 kB
>     Depends: libc6 (>= 2.15), libssl1.1 (>= 1.1.1)
>     Suggests: ca-certificates
>     Homepage: https://www.openssl.org/
>     Task: minimal
>     Supported: 5y
>     Download-Size: 613 kB
>     APT-Sources: http://us-west-2.ec2.archive.ubuntu.com/ubuntu bionic-updates/main amd64 Packages
>     Description: Secure Sockets Layer toolkit - cryptographic utility
>      This package is part of the OpenSSL project's implementation of the SSL
>      and TLS cryptographic protocols for secure communication over the
>      Internet.
>      .
>      It contains the general-purpose command line binary /usr/bin/openssl,
>      useful for cryptographic operations such as:
>       * creating RSA, DH, and DSA key parameters;
>       * creating X.509 certificates, CSRs, and CRLs;
>       * calculating message digests;
>       * encrypting and decrypting with ciphers;
>       * testing SSL/TLS clients and servers;
>       * handling S/MIME signed or encrypted mail.
>     
>     N: There are 3 additional records. Please use the '-a' switch to see them.

If not installed, `sudo apt install openssl`

---

generate self-signed certificate

Command to create a sefl-signed certificate - command will put key and cert if appropriate places
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt
```
Fill out the appropriate information (if desired)

---

add a new server to listen on https

`sudo vim /etc/nginx/nginx.conf`

Add the following server block as the last server block

>         server {
>             listen 443 ssl;
>             ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
>             ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;
>             return 200 "ccccceeeeeeeeeeeeeeert\n";
>         }

reload nginx to apply the changes `sudo nginx -s reload`

curl the site check it  `curl localhost:443`

>     ubuntu@ip-10-1-1-4:/var/www$ curl localhost:443
>     <html>
>     <head><title>400 The plain HTTP request was sent to HTTPS port</title></head>
>     <body bgcolor="white">
>     <center><h1>400 Bad Request</h1></center>
>     <center>The plain HTTP request was sent to HTTPS port</center>
>     <hr><center>nginx/1.14.0 (Ubuntu)</center>
>     </body>
>     </html>

It failed, why?   ***becuase we asked for a regular http site, not https***

try `curl -k https://localhost`

>     ubuntu@ip-10-1-1-4:/var/www$ curl -k https://localhost
>     ccccceeeeeeeeeeeeeeert

sucess!
