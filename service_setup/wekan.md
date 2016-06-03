# tomesh.net Kanban

The Toronto Mesh uses a [Kanban (看板)](https://en.wikipedia.org/wiki/Kanban) to keep track of ideas and their progess. The software we use is the self-hosted open-source [Wekan](https://github.com/wekan/wekan). Anyone is free to create an account and participate.

## Usage

You can contribute to the [Toronto Mesh](tomesh.net) project in many ways. Start by creating an account and login to the [Toronto Mesh Kanban](http://wekan.tomesh.net).

### Propose an Idea

* Create a new Card in the **Ideas** column by adding a short title
* Include details in the Description
* Add appropriate Labels for easy filtering

### Participate in Discussion

* You can add a Comment to an existing Card, regardless of what column the Card is in
* Visit [tomesh.net](https://tomesh.net) and find other chat channels to discuss

### Work on a Card

* Find a Card you would like to take ownership and add yourself as a Member to that Card
* Move the Card to the **In Progress** column, or **Discuss** column if that needs to happen first for the particular Card
* When completed, move the Card to the **Done** column (a task that leads to a Pull Request in our [Github repositories](https://github.com/tomeshnet/) is usually considered done when reviewed and merged)

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

1. Update the autostart script and reboot:

	```
	$ update-rc.d -f wekan remove && update-rc.d wekan defaults
	$ sudo reboot
	```

 	Find Wekan on [http://wekan.tomesh.net](http://wekan.tomesh.net).
