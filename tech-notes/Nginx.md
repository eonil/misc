Nginx
=====

How to Setup TLS/SSL
--------------------
Assumes you are using Ubuntu and Let's Encrypt.

Edit `/etc/nginx/sites-enabled/default.conf`.
Add something like these lines.

    server {
        listen 443 ssl;
        server_name yourdomain.here www.yourdomain.here;
        root /var/www/demo;
        ssl_certificate /etc/letsencrypt/live/yourdomain.here/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/yourdomain.here/privkey.pem;
    }

Don't forget to restart Nginx.

    sudo service nginx restart

[Source](https://letsecure.me/secure-web-deployment-with-lets-encrypt-and-nginx/)
