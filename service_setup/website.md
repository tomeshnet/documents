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
      server_name tomesh.net www.tomesh.net;
      return 301 https://$server_name$request_uri;
  }

  server {
      listen 443 ssl http2 default_server;
      listen [::]:443 ssl http2 default_server;
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