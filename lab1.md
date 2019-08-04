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
