# tomesh.net

We are self-hosting [tomesh.net](https://tomesh.net). This page describes how the server is set up.

## Set Up Server

1. Spin up a Virtual Machine (e.g. [DigitalOcean Droplet](http://digitalocean.com)) running **Ubuntu 16.04.1 x64**.

1. Secure your server and create non-root user with `sudo` by following [these instructions](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04).

1. Get a root shell by logging in and as non-root user, then run `sudo -i`.

1. Enable **ufw** firewall:

  ```
  # ufw allow ssh
  # ufw allow www
  # ufw enable
  # ufw status
  ```

1. Point the `tomesh.net` DNS A (and AAAA for IPv6) record to `YOUR_SERVER_IP`.

## Set up HTTPS with Nginx and Let's Encrypt

Follow [these instructions](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04) to set up nginx and letsencrypt.

### Configure Nginx

1. Create **/etc/nginx/sites-available/tomesh.net**:

  ```
  server {
    listen 80;
    server_name tomesh.net www.tomesh.net;
    return 301 https://$server_name$request_uri;
  }

  server {
    listen 443 ssl http2 default_server;
    listen [::]:443 ssl http2 default_server;
    include snippets/ssl-tomesh.net.conf;
    include snippets/ssl-params.conf;

    root /var/www/tomesh.net/html;

    error_page 404 /404/index.html;

    location = /404 {
      internal;
    }

    location / {
      try_files $uri $uri/ =404;
    }

    location ~ /.well-known {
      allow all;
    }

    location ~* \.(?:ttf|ttc|otf|eot|woff|woff2)$ {
      expires 1M;
      access_log off;
    }
  }
  ```

1. Symlink **/etc/nginx/sites-available/tomesh.net** to **/etc/nginx/sites-enabled**.

1. Check your configuration for syntax errors `nginx -t`.

1. Reload Nginx `service nginx reload`.

### Configure Let's Encrypt

1. Generate a Deffie-Hellman **.pem** and add the path to `ssl_dhparam` in Nginx configurations.

1. Run the **letsencrypt-auto** script:

  ```
  # /opt/letsencrypt/letsencrypt-auto certonly --agree-tos --renew-by-default --email hello@tomesh.net -a webroot --webroot-path=/var/www/html -d tomesh.net -d www.tomesh.net
  ```

1. In Nginx configurations, update `ssl_certificate`, `ssl_certificate_key`, `ssl_trusted_certificate` paths to the generated **.pem** files.

1. Reload Nginx `service nginx reload`.

1. Add the following to **crontab**:

  ```
  30 2 * * 1 /opt/letsencrypt/letsencrypt-auto renew >> /var/log/le-renew.log
  35 2 * * 1 /bin/systemctl reload nginx
  ```

## Set up jekyll-hook and build script

We use webhooks from Github to generate the Jekyll site on our server with [jekyll-hook](https://github.com/developmentseed/jekyll-hook).

### Clone tomesh.net

1. Clone tomesh.net reprository `git clone https://github.com/tomeshnet/tomesh.net.git`

1. `cd tomesh.net`

1. `chmod +x script/tomesh-build.sh`

1. Note expected directory it will use to clone `master`.

### Set up jekyll-hook

1. Install jekyll-hook's dependencies as [noted here](https://github.com/developmentseed/jekyll-hook#dependencies-installation).

1. Clone jekyll-hook's reprository (`/var/www/jekyll-hook`) and run `npm install`. [Noted here](https://github.com/developmentseed/jekyll-hook#installation)

1. Create a symbolic link to `tomesh-build.sh` in jekyll-hook's `scripts` directory:

  ```
  ln -s ~/tomesh.net/scripts/tomesh-build.sh scripts/
  ```

1. Edit jekyll-hook `config.json` to use `tomesh-build.sh` as the default publish script and allow webhooks from tomeshnet organization:

  ```
  {
      "gh_server": "github.com",
      "temp": "/var/www/jekyll-hook",
      "public_repo": true,
      "scripts": {
        "#default": {
          "build": "./scripts/build.sh",
          "publish": "./scripts/tomesh-build.sh"
        }
      },
      "secret": "",
      "email": {
          "isActivated": false,
          "user": "",
          "password": "",
          "host": "",
          "ssl": true
      },
      "accounts": [
          "tomeshnet"
      ]
  }
  ```

1. Launch in background `forever start jekyll-hook.js`. [Noted here](https://github.com/developmentseed/jekyll-hook#launch)

1. Update UFW to allow TCP connections on port 8080 `ufw allow 8080/tcp`.
