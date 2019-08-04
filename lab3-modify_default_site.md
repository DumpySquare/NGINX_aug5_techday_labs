

We are going to modify the default site for demo purposes

on the command line of the linux host we just installed nginx on,

`sudo vim /var/www/html/index.nginx-debian.html`

to modify the html title tag 
1. i to enter insert mode
2. make modification
3. then ESC
4. :x ENTER (to write and quit)

```
original | <title>Welcome to nginx!</title>
modified | <title>***PS-default*** nginx!</title>
```

Check nginx config syntax

`sudo nginx -t`

reload nginx to load new configuration

`sudo nginx -s reload`

---
use curl againt to get updated local site

`curl localhost`

>     ubuntu@ip-10-1-1-4:/$ curl localhost
>     <!DOCTYPE html>
>     <html>
>     <head>
>     <title>***PS-default*** nginx!</title>
>     <style>
>         body {
>             width: 35em;
>             margin: 0 auto;
>             font-family: Tahoma, Verdana, Arial, sans-serif;
>         }
>     </style>
>     </head>
>     <body>
>     <h1>Welcome to nginx!</h1>
>     <p>If you see this page, the nginx web server is successfully installed and
>     working. Further configuration is required.</p>
>     
>     <p>For online documentation and support please refer to
>     <a href="http://nginx.org/">nginx.org</a>.<br/>
>     Commercial support is available at
>     <a href="http://nginx.com/">nginx.com</a>.</p>
>     
>     <p><em>Thank you for using nginx.</em></p>
>     </body>
>     </html>
