# nginxamples
 Examples of Nginx configuration.

# 1. Config with Django & Vue.js
```
# /etc/nginx/sites-enabled/djangovue.conf

upstream django {
    server unix:///home/f'{username}'/repos/f'{repo_name}'/uwsgi/socket/f'{repo_name}'.sock;
}

server {
    listen 80 default_server;
    return 403;
}

server {
    listen 80;
    server_name f'{domain_name}';
    charset utf-8;
    client_max_body_size 10M;

    location /static {
        alias /home/f'{username}'/repos/f'{repo_name}'/static;
    }

    location /media {
        alias /home/f'{username}'/repos/f'{repo_name}'/media;
    }

    location / {
        uwsgi_pass django;
        include /etc/nginx/uwsgi_params;
    }

    location / {
        root /home/f'{username}'/repos/f'{repo_name}'/dist;
        index index.html;
        try_files $uri $uri/ /index.html;
    }
}
```
