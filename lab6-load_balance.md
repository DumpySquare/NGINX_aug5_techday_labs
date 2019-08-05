
---

next lets do some load balancing with ssl offload

`sudo vim /etc/nginx/nginx.conf`

Update three (3) things:
1.  add the upstream directive for ***mypool*** 
2.  Update server listening on 81 to `return 301 https://$host$request_uri`
3.  Add final server directive for ***444***

Full http block below
```
http {
    upstream mypool1 {
        server localhost:82;
        server localhost:83;
    }

    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;

    server {
        listen 81;
        return 301 https://$host$request_uri;
    }

    server {
        listen 82;
        root /var/www;
        index site1.html;
    }

    server {
        listen 83;
        return 200 "this server listens on 83\n";
    }

    server {
        listen 443 ssl;
        ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
        ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;
        return 200 "ccccceeeeeeeeeeeeeeert\n";
    }

   server {
        listen 444 ssl;
        ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
        ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;
        location / {
            proxy_pass http://mypool1;
        }
}
```

reload nginx  `sudo nginx -s reload`

try new changes

This one works to default page
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

This broke, but just becuase we didn't follow the redirect to https
>     ubuntu@ip-10-1-1-4:/var/www$ curl localhost:81
>     <html>
>     <head><title>301 Moved Permanently</title></head>
>     <body bgcolor="white">
>     <center><h1>301 Moved Permanently</h1></center>
>     <hr><center>nginx/1.14.0 (Ubuntu)</center>
>     </body>
>     </html>
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

This one worked
>     ubuntu@ip-10-1-1-4:/var/www$ curl localhost:83
>     this server listens on 83


This one worked over https
>     ubuntu@ip-10-1-1-4:/var/www$ curl -k https://localhost:443
>     ccccceeeeeeeeeeeeeeert

First call to 444 hit the first server in the pool
>     ubuntu@ip-10-1-1-4:/var/www$ curl -k https://localhost:444
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
  
  
Second call to 444 sent us to the second pool member
>     ubuntu@ip-10-1-1-4:/var/www$ curl -k https://localhost:444
>     this server listens on 83

yay!
