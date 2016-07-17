# tomesh.net Kanban

We are self-hosting [Wekan](https://github.com/wekan/wekan) to coordinate tasks. This page describes how the Wekan server is set up.

## Set Up Wekan Server

1. Spin up a Virtual Machine (e.g. [DigitalOcean Droplet](http://digitalocean.com)) running **Ubuntu 14.04.4 x64**.

1. Login as the **root** user.

1. Enable **ufw** firewall:

	```
	$ ufw allow ssh
	$ ufw allow www
	$ ufw enable
	$ ufw status
	```

1. Install Wekan with the [auto-install script](https://raw.githubusercontent.com/tomeshnet/wekan/v0.10.1/autoinstall_wekan.sh) we forked from [anselal/wekan](https://github.com/anselal/wekan/) and reboot:

	```
	$ wget https://raw.githubusercontent.com/tomeshnet/wekan/v0.10.1/autoinstall_wekan.sh
	$ chmod +x autoinstall_wekan.sh
	$ ./autoinstall_wekan.sh
	```

	Confirm Wekan is running on **http://YOUR_SERVER_IP:8080**

1. Point the `wekan.tomesh.net` DNS A (and AAAA for IPv6) record to `YOUR_SERVER_IP`.

1. In **/etc/init.d/wekan**, change `ROOT_URL` and `PORT` to:

	```
	export ROOT_URL="http://wekan.tomesh.net"
	export PORT="80"
	```

1. Update the auto-start script and reboot:

	```
	$ update-rc.d -f wekan remove && update-rc.d wekan defaults
	$ reboot
	```

 	Find Wekan on [http://wekan.tomesh.net](http://wekan.tomesh.net).
