# tomesh.net Chat

Toronto Mesh is running a [Matrix](http://matrix.org) homeserver for our decentralized chat. The Matrix protocol allows us to communicate on the same homeserver, as well as reach users and rooms on other homeservers via homeserver federation. Users are free to connect to our homeserver with [any compatible desktop or mobile client](http://matrix.org/docs/projects/try-matrix-now.html#clients), or the web client we host.

**Matrix homeserver**: [https://matrix.tomesh.net](https://matrix.tomesh.net)
**Web client**: [https://chat.tomesh.net](https://chat.tomesh.net)

This page describes how both these components are set up.

## Set Up Martix Homeserver

We currently run the Python-implemented [Synapse](https://github.com/matrix-org/synapse/) homeserver at **matrix.tomesh.net**.

### Install Synapse Homeserver

1. Get a root shell with `sudo -i`.

1. Install the tools:

	```
	sudo apt-get install build-essential python2.7-dev libffi-dev \
	                     python-pip python-setuptools sqlite3 \
	                     libssl-dev python-virtualenv libjpeg-dev libxslt1-dev
	```

1. Install Synapse homeserver at commit [5405351b147cb5e1b62651fd0c5ad95c5e0569e6](https://github.com/matrix-org/synapse/commit/5405351b147cb5e1b62651fd0c5ad95c5e0569e6):

	```
	# virtualenv -p python2.7 ~/.synapse
	# source ~/.synapse/bin/activate
	# pip install --upgrade setuptools
	# pip install https://github.com/matrix-org/synapse/tarball/5405351b147cb5e1b62651fd0c5ad95c5e0569e6
	```

	>From now on, each time you want to configure the server, run `cd ~/.synapse && source ./bin/activate` from a root shell.

1. Set up the homeserver in our virtualenv:

	```
	# cd ~/.synapse
	# python -m synapse.app.homeserver \
	    --server-name tomesh.net \
	    --config-path homeserver.yaml \
	    --generate-config \
	    --report-stats=no
	```

1. Enable registration for new users by changing `enable_registration` to `True` in **homeserver.yaml**.

1. To prevent our 1 GB VPS from running out of memory, we need to reduce the cache factor by running:

	```
	echo "synctl_cache_factor: 0.02" >> homeserver.yaml
	```

1. Synapse keeps a lot of logs by default. Open up **tomesh.net.log.config**, find `handlers:file:backupCount` and change the value to `1`.

1. Start the server with `synctl start`.

	>If you want to stop the server at some point, run `synctl stop`.

### Set Up Federation

1. Due to a current IPv6 limitation in a Synapse dependency, we must resolve DNS through IPv4 for federation to work. Edit **/etc/network/interfaces** and comment out the `dns-nameservers` line, then add a line with only the IPv4 DNS nameserver:

    ```
    #        dns-nameservers 2001:4860:4860::8844 2001:4860:4860::8888 8.8.8.8
            dns-nameservers 8.8.8.8
    ```

1. Reboot the server with `sudo reboot`. Then verify **/etc/resolv.conf** only contains IPv4 DNS servers.

1. Create a SRV record and publish it in DNS:

	```
	$ dig -t srv _matrix._tcp.tomesh.net
	_matrix._tcp    IN      SRV     10 0 8448 matrix.tomesh.net.
	```

1. Open up firewall for federation over port 8448 `ufw allow 8448`.

### Set up HTTPS with nginx and letsencrypt

1. If nginx and letsencrypt aren't already installed on the server, see [our Wekan setup](https://github.com/tomeshnet/documents/blob/master/service_setup/wekan.md) to configure the basics.

1. Create **/etc/nginx/sites-available/matrix.tomesh.net**:

	```
	server {
	    listen 80;
	    server_name matrix.tomesh.net;
	    return 301 https://$host$request_uri;
	}

	server {
	    listen 443 ssl;
	    server_name matrix.tomesh.net;

	    ssl_certificate /etc/letsencrypt/live/matrix.tomesh.net/fullchain.pem;
	    ssl_certificate_key /etc/letsencrypt/live/matrix.tomesh.net/privkey.pem;
	    ssl_trusted_certificate /etc/letsencrypt/live/matrix.tomesh.net/fullchain.pem;

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
	        proxy_pass http://127.0.0.1:8008/;
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

1. Start serving the site by symlinking:

	```
	ln -s /etc/nginx/sites-available/matrix.tomesh.net /etc/nginx/sites-enabled/matrix.tomesh.net
	```
1. Reload nginx `service nginx reload`.

1. Assuming Deffie-Hellman **.pem** and **crontab** for letsencrypt renewals are already configured, just run:

	```
	# /opt/letsencrypt/letsencrypt-auto certonly --agree-tos --renew-by-default --email hello@tomesh.net -a webroot --webroot-path=/usr/share/nginx/html -d matrix.tomesh.net
	```

### Update Synapse Version

1. Enter the virtualenv from a root shell:

	```
	# cd ~/.synapse
	# source ./bin/activate
	```
1. Stop the Synapse server with `synctl stop`.

1. Update with the following command where `VERSION` can be a branch like `master` or `develop`, or a release tag like `v0.17.1`, or a commit hash:

	```
	# pip install --upgrade --process-dependency-links https://github.com/matrix-org/synapse/tarball/VERSION
	```

1. Start the Synapse server again with `synctl start`.

## Set Up Vector Web Client

The web client we host at **chat.tomesh.net** is running [Vector Web](https://github.com/vector-im/vector-web), and defaults to use our Matrix homeserver.

### Build Vector Web From Source

1. Use [nvm](https://github.com/creationix/nvm) to get these versions of **node.js** and **npm**:

	```
	$ node -v
	v6.4.0
	$ npm -v
	3.10.3
	```

1. Follow instructions on the [Vector Web Github repo](https://github.com/vector-im/vector-web/) to build a package of the static files. Basically, run the following commands to build **v0.7.4**:

	```
	$ git clone https://github.com/vector-im/vector-web.git
	$ cd vector-web
	$ git checkout v0.7.4
	$ npm install
	$ npm run package
	```

1. Find the generated package at **packages/vector-v0.7.4.tar.gz**.

### Serve Vector Web at chat.tomesh.net

1. Get a root shell with `sudo -i`.

1. Extract **vector-v0.7.4.tar.gz** into **/var/www/chat.tomesh.net**.

1. Create **config.json** from the sample with `cp config.sample.json config.json`, then edit `default_hs_url` in **config.json** such that the file looks like:

```
{
    "default_hs_url": "https://matrix.tomesh.net",
    "default_is_url": "https://vector.im",
    "brand": "Vector",
    "integrations_ui_url": "http://localhost:8081/",
    "integrations_rest_url": "http://localhost:5050",
    "enableLabs": true
}
```

1. Run `chmod 755 /var/www` to ensure we have the right permissions.

### Set up HTTPS with nginx and letsencrypt

1. If nginx and letsencrypt aren't already installed on the server, see [our Wekan setup](https://github.com/tomeshnet/documents/blob/master/service_setup/wekan.md) to configure the basics.

1. Create **/etc/nginx/sites-available/chat.tomesh.net**:

	```
	server {
	    listen 80;
	    server_name chat.tomesh.net;
	    return 301 https://$host$request_uri;
	}

	server {
	    listen 443 ssl;
	    server_name chat.tomesh.net;

	    root /var/www/chat.tomesh.net/public;
	    index index.html index.htm;

	    ssl_certificate /etc/letsencrypt/live/chat.tomesh.net/fullchain.pem;
	    ssl_certificate_key /etc/letsencrypt/live/chat.tomesh.net/privkey.pem;
	    ssl_trusted_certificate /etc/letsencrypt/live/chat.tomesh.net/fullchain.pem;

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
	        try_files $uri $uri/ =404;
	    }
	}
	```

1. Start serving the site by symlinking:

	```
	ln -s /etc/nginx/sites-available/chat.tomesh.net /etc/nginx/sites-enabled/chat.tomesh.net
	```

1. Reload nginx `service nginx reload`.

1. Assuming Deffie-Hellman **.pem** and **crontab** for letsencrypt renewals are already configured, just run:

	```
	# /opt/letsencrypt/letsencrypt-auto certonly --agree-tos --renew-by-default --email hello@tomesh.net -a webroot --webroot-path=/usr/share/nginx/html -d chat.tomesh.net
	```

