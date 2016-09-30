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
  upstream backend {
      server 127.0.0.1:80;
  }

  server {
      listen 80;
      server_name wekan.tomesh.net;

      # Add headers to serve security related headers
      add_header X-Content-Type-Options nosniff;
      add_header X-Frame-Options "SAMEORIGIN";
      add_header X-XSS-Protection "1; mode=block";
      add_header X-Robots-Tag none;
      add_header X-Download-Options noopen;
      add_header X-Permitted-Cross-Domain-Policies none;

      location / {
          proxy_pass http://127.0.0.1:8080/;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "upgrade";
          proxy_set_header Host $http_host;

          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forward-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forward-Proto http;
          proxy_set_header X-Nginx-Proxy true;

          proxy_redirect off;
      }

      location ~ /.well-known {
          allow all;
      }
  }

  server {
      listen 443 ssl;
      server_name wekan.tomesh.net;

      ssl_certificate /etc/letsencrypt/live/wekan.tomesh.net/fullchain.pem;
      ssl_certificate_key /etc/letsencrypt/live/wekan.tomesh.net/privkey.pem;
      ssl_trusted_certificate /etc/letsencrypt/live/wekan.tomesh.net/fullchain.pem;

      ssl_session_timeout 1d;
      ssl_session_cache shared:SSL:50m;

      # Diffie-Hellman parameter for DHE ciphersuites, recommended 2048 bits
      # Generate with: openssl dhparam -out /etc/nginx/dhparam.pem 4048
      ssl_dhparam /etc/ssl/certs/dhparam.pem;

      # Mozilla "Intermediate configuration" copied from https://mozilla.github.io/server-side-tls/ssl-config-generator/
      ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
      ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-RSA-DES-CBC3-SHA:ECDHE-ECDSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
      ssl_prefer_server_ciphers on;

      # HSTS (ngx_http_headers_module is required) (15768000 seconds = 6 months)
      add_header Strict-Transport-Security max-age=15768000;

      # OCSP Stapling: fetch OCSP records from URL in ssl_certificate and cache them
      ssl_stapling on;
      ssl_stapling_verify on;

      # Add headers to serve security related headers
      add_header X-Content-Type-Options nosniff;
      add_header X-Frame-Options "SAMEORIGIN";
      add_header X-XSS-Protection "1; mode=block";
      add_header X-Robots-Tag none;
      add_header X-Download-Options noopen;
      add_header X-Permitted-Cross-Domain-Policies none;

      location / {
          proxy_pass http://127.0.0.1:80/;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "upgrade";
          proxy_set_header Host $http_host;

          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forward-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forward-Proto http;
          proxy_set_header X-Nginx-Proxy true;

          proxy_redirect off;
      }
  }
  ```

1. Symlink **/etc/nginx/sites-available/tomesh.net** to **/etc/nginx/sites-enabled**.

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