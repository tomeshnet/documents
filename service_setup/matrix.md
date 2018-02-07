# tomesh.net Chat

Toronto Mesh is running a [Matrix](http://matrix.org) homeserver for our decentralized chat. The Matrix protocol allows us to communicate on the same homeserver, as well as reach users and rooms on other homeservers via homeserver federation. Users are free to connect to our homeserver with [any compatible desktop or mobile client](http://matrix.org/docs/projects/try-matrix-now.html#clients), or the web client we host.

**Matrix homeserver**: [https://matrix.tomesh.net](https://matrix.tomesh.net)

**Web client**: [https://chat.tomesh.net](https://chat.tomesh.net)

This page describes how both these components are set up.

## Set Up Matrix Homeserver

We currently run the Python-implemented [Synapse](https://github.com/matrix-org/synapse/) homeserver at **matrix.tomesh.net**.

### Install Synapse Homeserver

1. Get a root shell with `sudo -i`.

1. Install the tools:

	```
	sudo apt-get install build-essential python2.7-dev libffi-dev \
	                     python-pip python-setuptools sqlite3 \
	                     libssl-dev python-virtualenv libjpeg-dev libxslt1-dev
	```

1. Install Synapse homeserver version [v0.19.2](https://github.com/matrix-org/synapse/releases/tag/v0.19.2):

	```
	# virtualenv -p python2.7 ~/.synapse
	# source ~/.synapse/bin/activate
	# pip install --upgrade setuptools
	# pip install https://github.com/matrix-org/synapse/tarball/v0.19.2
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

1. Enable guest access to public rooms by changing `allow_guest_access` to True` in **homeserver.yaml**.

1. Enable link preview by changing `url_preview_enabled` to `True` in **homeserver.yaml** and uncommenting:

	```
	url_preview_ip_range_blacklist:
	- '127.0.0.0/8'
	- '10.0.0.0/8'
	- '172.16.0.0/12'
	- '192.168.0.0/16'
	```
	
	You also need to `pip install lxml` to start Synapse with link preview.

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

        location ~ /.well-known {
          allow all;
          root /usr/share/nginx/html;
        }
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

        location ~ /.well-known {
          allow all;
          root /usr/share/nginx/html;
        }

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

1. Assuming Diffie-Hellman **.pem** and **crontab** for letsencrypt renewals are already configured, just run:

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

### Migrate Database to PostgreSQL

At some point we migrated our SQLite database to PostgreSQL for better performance:

1. Back up a snapshot of the VM, and then copy the Synapse files, including the SQLite database, to another directory.

1. [Install PostgreSQL](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-14-04) on the VM and [verify its security settings](https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps).

1. Create the `synapse_user` PostgreSQL user, set a `PASSWORD` and give it permissions to the `synapse` database.

1. Follow the [migration instructions from Synapse](https://github.com/matrix-org/synapse/blob/master/docs/postgres.rst#synapse-config), replacing the `database` section in **homeserver.yaml** with:

	```
	# Postgres database configuration
	database:
	    name: psycopg2
	    args:
	        user: synapse_user
	        password: PASSWORD
	        database: synapse
	        host: localhost
	        cp_min: 5
	        cp_max: 10
	```

### Synapse Performance Bug

Our version of Synapse homeserver accumulates forward extremities over time due to [a known bug](https://github.com/matrix-org/synapse/issues/1760). The current workaround is to perform the following steps when performance suffers noticably:

1. SSH into **tomesh0**

1. Switch to Synapse Postgres user `sudo -i -u synapse_user`

1. Load CLI and connect to Synapse database `psql -d synapse`

1. Run query and look for rooms with more than 3 forward extremities:

	```
	select room_id, count(*) c from event_forward_extremities group by room_id order by c desc limit 5;
	```

1. Run the following for each of the high extremities room:

	```
	DELETE FROM event_forward_extremities AS e
	USING ( 
	    SELECT DISTINCT ON (room_id)
	    room_id,
	    last_value(event_id) OVER w AS event_id
	    FROM event_forward_extremities
	    NATURAL JOIN events
	    WINDOW w AS (
	        PARTITION BY room_id
	        ORDER BY stream_ordering
	        range between unbounded preceding and unbounded following
	    )
	    ORDER BY room_id, stream_ordering
	) AS s
	WHERE
	    s.room_id = e.room_id
	    AND e.event_id != s.event_id
	    AND e.room_id = '!jpZMojebDLgJdJzFWn:matrix.org';
	```

1. Run the select again to confirm that forward extremities counts are cleared up for all those rooms. Restart Synapse and the Droplet dashboard should show much lower resource usage.

## Set Up Riot Web Client

The web client we host at **chat.tomesh.net** is running [Riot Web](https://github.com/vector-im/riot-web), and defaults to use our Matrix homeserver.

### Serve Riot Web at chat.tomesh.net

1. Get a root shell with `sudo -i`.

1. Download the pre-compiled [Riot Web release](https://github.com/vector-im/riot-web/releases):

	```
	# wget https://github.com/vector-im/riot-web/releases/download/v0.9.5/vector-v0.9.5.tar.gz
	```

1. Extract **vector-v0.9.5.tar.gz** into **/var/www/chat.tomesh.net/public**:

	```
	# tar xf vector-v0.9.5.tar.gz -C /var/www/chat.tomesh.net/public --strip-components 1
	```

1. Create **config.json** with the following lines, so it is used in place of the default **config.sample.json**:

	```
	{
	    "default_hs_url": "https://matrix.tomesh.net",
	    "default_is_url": "https://vector.im",
	    "brand": "Riot",
	    "integrations_ui_url": "https://scalar.vector.im/",
	    "integrations_rest_url": "https://scalar.vector.im/api",
	    "enableLabs": true,
	    "roomDirectory": {
	        "servers": [
	            "tomesh.net",
	            "nycmesh.net",
	            "matrix.org"
	        ]
	    }
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

1. Assuming Diffie-Hellman **.pem** and **crontab** for letsencrypt renewals are already configured, just run:

	```
	# /opt/letsencrypt/letsencrypt-auto certonly --agree-tos --renew-by-default --email hello@tomesh.net -a webroot --webroot-path=/usr/share/nginx/html -d chat.tomesh.net
	```
	
## Create More RAM

We are running Synapse on a 1 GB VPS that also runs other services. The process often gets dangerously close to being killed by the kernel from memory exhaustion. So we created 2 GB of swap memory on the SSD to handle load spikes:

```
# dd if=/dev/zero of=/swapfile bs=1M count=2048
# chmod 600 /swapfile
# mkswap /swapfile
# swapon /swapfile
# echo '/swapfile none swap defaults 0 0' >> /etc/fstab
```
