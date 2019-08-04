start with a ubuntu 18.04 desktop installation
- I typically do the stripped down version, minimal gui, no extra apps


Depending on setup you may need to install ssh server to access server on network:

```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl status ssh
```
I like vim, so... `sudo apt install vim` if needed

install nginx

`sudo apt install nginx`

See what version of nginx got installed

` sudo nginx -v `

>     ubuntu@ip-10-1-1-4:/$ sudo nginx -v
>     nginx version: nginx/1.14.0 (Ubuntu)

Show apt version of what got installed

` sudo apt show nginx `

>       ubuntu@ip-10-1-1-4:/$ sudo apt show nginx
>       Package: nginx
>       Version: 1.14.0-0ubuntu1.3
>       Priority: optional
>       Section: web
>       Origin: Ubuntu
>       Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
>       Original-Maintainer: Debian Nginx Maintainers <pkg-nginx-maintainers@lists.alioth.debian.org>
>       Bugs: https://bugs.launchpad.net/ubuntu/+filebug
>       Installed-Size: 43.0 kB
>       Depends: nginx-core (<< 1.14.0-0ubuntu1.3.1~) | nginx-full (<< 1.14.0-0ubuntu1.3.1~) | nginx-light (<< 1.14.0-0ubuntu1.3.1~) | nginx-extras (<< 1.14.0-0ubuntu1.3.1~), nginx-core (>= 1.14.0-0ubuntu1.3) | nginx-full (>= 1.14.0-0ubuntu1.3) | nginx-light (>= 1.14.0-0ubuntu1.3) | nginx-extras (>= 1.14.0-0ubuntu1.3)
>       Homepage: http://nginx.net
>       Supported: 5y
>       Download-Size: 3596 B
>       APT-Manual-Installed: yes
>       APT-Sources: http://us-west-2.ec2.archive.ubuntu.com/ubuntu bionic-updates/main amd64 Packages
>       Description: small, powerful, scalable web/proxy server
>        Nginx ("engine X") is a high-performance web and reverse proxy server
>        created by Igor Sysoev. It can be used both as a standalone web server
>        and as a proxy to reduce the load on back-end HTTP or mail servers.
>        .
>        This is a dependency package to install either nginx-full (by default),
>        nginx-light or nginx-extras.
>       
>       N: There are 2 additional records. Please use the '-a' switch to see them.
