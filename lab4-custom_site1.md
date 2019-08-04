Change to directory where websites are held

`cd /var/www/`

Download a little custom html page

`sudo curl -O https://raw.githubusercontent.com/DumpySquare/aug5_techday/master/site1.html`

>     ubuntu@ip-10-1-1-4:/var/www$ sudo curl -O https://raw.githubusercontent.com/DumpySquare/aug5_techday/master/site1.html
>       % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
>                                      Dload  Upload   Total   Spent    Left  Speed
>     100   276  100   276    0     0   1164      0 --:--:-- --:--:-- --:--:--  1164

modify nginx config to use new html file and add some other listening servers

sudo vim /etc/nginx/nginx.conf

Add the following server blocks in the http context, above the current listen 83 server
>        server {
>            listen 81;
>            return 200 "hostess with tha mostess on 81\n";
>        }
>    
>        server {
>            listen 82;
>            root /var/www;
>            index site1.html;
>        }

reload nginx config     `sudo nginx -s reload`

check websites

>     curl localhost
>     curl localhost:81
>     curl localhost:82
>     curl localhost:83

This is what you should get


>     ubuntu@ip-10-1-1-4:/var/www$ curl localhost
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
>     ubuntu@ip-10-1-1-4:/var/www$ curl localhost:81
>     hostess with tha mostess on 81
>     ubuntu@ip-10-1-1-4:/var/www$ curl localhost:82
>     <!DOCTYPE html>
>     <html>
>     <head>
>     <title>site1-F5-PS-Rocks!!!</title>
>     <style>
>         body {
>             width: 35em;
>             margin: 0 auto;
>             font-family: Tahoma, Verdana, Arial, sans-serif;
>         }
>     </style>
>     <body>
>     <h1>Is it the F5?</h1>
>     <p>ONLY if it fixed it!</p>
>     </body>
>     </html>
>     ubuntu@ip-10-1-1-4:/var/www$ curl localhost:83
>     this server listens on 83
