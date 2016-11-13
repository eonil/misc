Nginx
=====

How to Setup TLS/SSL
--------------------
Assumes you are using Ubuntu and Let's Encrypt.

Edit `/etc/nginx/sites-enabled/default.conf`.
Add something like these lines.

    server {
        listen 443 ssl default_server;
        server_name my-domain;

        ssl_certificate /etc/letsencrypt/live/my-domain/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/my-domain/privkey.pem;

        ...
    }

Don't forget to restart Nginx.

    sudo service nginx restart

[Source](https://www.nginx.com/blog/free-certificates-lets-encrypt-and-nginx/)


