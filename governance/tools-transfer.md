# Tools Transfer Guide

## Outline
This page describes the services that the tomesh tools team is responsible for.
The acting team may use this document as a reference whenever there is a transfer of responibilities to a new group.
Contact the tools team for further details.

## Tools Team Responsibilities
The tomesh tools team is responsible for managing the following:

### Website
- Server: All the files are hosted on the tomesh1 [Digital Ocean](https://www.digitalocean.com) droplet.
- DNS: [hover](www.hover.com) is the DNS service provider. This service allows us to map tomesh.net to the IP address of the tomesh1 droplet.
- Github: The [tomesh.net repository](https://github.com/tomeshnet/tomesh.net) hosts the website files.
- Build A Node page is pulled from (prototype-cjdns-pi)[https://github.com/tomeshnet/prototype-cjdns-pi] README.md

Webhook is configured in Github to ping the server on push. 
The droplet pulls its content from the Github repository periodically and whenever it is pinged.  
The droplet uses nginx and Let's Encrypt to serve content over HTTPS.  
nginx decides what content to serve depending on what domain the request is coming from.

#### Map on Website 
- Map Uses GOOGLE MAP API 
- Current Google API Key: AIzaSyDfjIeSSWeDLOYt7f_cHHG4GtgOowvQFBs
- New key can be obtained from [Google](https://developers.google.com/maps/documentation/javascript/get-api-key)
- Nodes are populated from Github repository [node-list](https://github.com/tomeshnet/node-list)

### Collaboration: Chat
tomesh uses a Matrix chat server to provide a communication platform.
- Server: The Matrix server and Web Client are hosted on the tomesh0 [Digital Ocean](https://www.digitalocean.com) droplet.
- DNS: [hover](www.hover.com) is the DNS service provider. This service allows us to map chat.tomesh.net to the IP address of the tomesh0 droplet.

See the Matrix page of the service setup section for further details.

### Collaboration: Wekan
A Wekan kanban board is maintained for all projects and ideas being worked on.
- Server: The Wekan server is hosted on the tomesh0 [Digital Ocean](https://www.digitalocean.com) droplet.
- DNS: [hover](www.hover.com) is the DNS service provider. This service allows us to map chat.tomesh.net to the IP address of the tomesh0 droplet.

See the Wekan page of the service setup section for further details.

### Email
- Server: The Email server is hosted by [Seattle Mesh](https://seattlemesh.net/). Finn is the current point of contact.
- DNS: [hover](www.hover.com) is the DNS service provider. This service allows us to map webmail.tomesh.net to the IP address of the email server.

See the Email page in the service setup section for further details.

## Team Transfers: Website and Collaboration Tools
[Digital Ocean](https://www.digitalocean.com/)  
The new team needs to generate user accounts and ssh key pairs or passwords for both tomesh0 and tomesh1 droplets.
Additionally, the new team members may get added to the tomesh Digital Ocean group. 

## Team Transfers: Email
[Postfix Admin](https://q.meshwith.me/postfixadmin/login.php)  
The new team needs to get admin credentials to the email server, add their names to the relevant aliases (VirtualList -> add MailBox), and create addresses if desired.  
When people are added or removed, the Tool channel must be notified of who is on which list.  
All accounts' passwords can be reset through the config panel.

## Team Transfers: Github
[tomesh Github page](https://github.com/tomeshnet)  
Members of the new team must become owners of the tomeshnet organization.
