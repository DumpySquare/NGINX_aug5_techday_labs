# aug5_techday
Tech day files

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

Show apt version of what got installed

` sudo apt show nginx `


Command to create a sefl-signed certificate
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt
```

https://github.com/trimstray/nginx-admins-handbook
