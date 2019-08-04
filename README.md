# aug5_techday
Tech day files


Command to create a sefl-signed certificate
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt
```

https://github.com/trimstray/nginx-admins-handbook
