
backup the original nginx config file - move it to a new name

`sudo mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.old`

make new nginx config file with the original name:

`sudo vim /etc/nginx/nginx.conf`

Add the following lines to the config file

>     user www-data;
>     worker_processes auto;
>     pid /run/nginx.pid;
>     include /etc/nginx/modules-enabled/*.conf;
>     
>     events {
>             worker_connections 768;
>     }
>     
>     http {
>         access_log /var/log/nginx/access.log;
>         error_log /var/log/nginx/error.log;
>         include /etc/nginx/conf.d/*.conf;
>         include /etc/nginx/sites-enabled/*;
>     
>         server {
>             listen 83;
>             return 200 "this server listens on 83\n";
>         }
>     }

save and exit -> `ESC` -> `:x ENTER`

`sudo nginx -s reload` -> to reload the config

`curl localhost:83` to call the server listening on port83

>     ubuntu@ip-10-1-1-4:/$ curl localhost:83
>     this server listens on 83
