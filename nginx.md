# Nginx notes / info / pain
## Commands
Start (ubuntu)
`service nginx start`

Stop / Reload / reopen
`nginx -s <command>`

## Config
* [Configuring express](http://blog.danyll.com/setting-up-express-with-nginx-and-pm2/)

## Basic multi-app Config
`server {
    listen       8080;
    server_name  localhost;

    # Proxy settings for all the proxied projects
    proxy_set_header HOST $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

    # node projects
    location /app1/ {
      proxy_pass http://localhost:1337/;
    }

    # load guilty pleas assets using nginx instead of express
    location /app1/static {
      alias /url/to/app1;
    }

    location /app2/ {
      proxy_pass http://localhost:3000/;
    }

    # load guilty pleas assets using nginx instead of express
    location /app2/static {
      alias /url/to/app2;
    }
}`
