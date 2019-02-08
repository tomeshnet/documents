---
title: Mesh Sync Notes - Jan 21, 2019
location: https://appear.in/tomeshnet
date: 2019-01-21
startTime: 10:00
endTime: 12:00
---

📍 https://appear.in/tomeshnet  
📅 Monday, January 21  

| Timezone | Workshop | General  |
|:---------|:---------|:---------|
| PST      |`07:00 am`|`08:00 am`|
| EST      |`10:00 am`|`11:00 am`|
| CEST     |`04:00 pm`|`05:00 pm`|
| HKT      |`10:00 pm`|`11:00 pm`|

## What is this?

Biweekly standing open-call for remote parties to sync up on topics of mutual interest. The hours are selected to make it possible for parties of different timezones to attend.

Anyone may propose a topic on [this open-edit pad](https://hackmd.io/HSOK15u7TnS6Oz1RH0McGg), taking one of six timeslots by putting yourself as _Facilitator_ and filling the corresponding [_Agenda_](#Agenda) section.

The _Course_ hour is for topics relating to the [Building the Peer-to-Peer Internet workshop series](https://tomeshnet.github.io/p2p-internet-workshop/), such as discussing about workshop facilitation at a new location, the logistics of getting the hardware and software set up, funding opportunities for curriculum development, etc.

The _General_ hour is for all other issues, such as [Prototype](https://github.com/tomeshnet/prototype-cjdns-pi) or [Mesh Orange](https://github.com/tomeshnet/mesh-orange) updates, IPFS live streaming discussions, showcasing your new project, or collective brainstorming of collaboration opportunities with Toronto Mesh.

Lastly, please scope your session within a 20 minute time block. If more time is needed, it is probably best to use the 20 minutes to give an overview then schedule separate meetings with interested parties. The hope is that these standing hours can be well attended and everyone participating gets a general idea of the things going on :satellite: 

## Attending

📝 This person moves meeting notes to GitHub and resets the pad:
- benhylau

👥 Please add your name to this list if attending:
- benhylau
- Zenna // @zelf
- sgo
- Tim
- Jacob // Powersource
- elon
- yurko

## Agenda

| Start time   | 20-min timeslot | Facilitator |
|:-------------|:----------------|:------------|
|`10:00 am EST`| Course 1        | benhylau    |
|              | Course 2        | tim         |
|              | Course 3        | darkdrgn2k  |
|`11:00 am EST`| General 1       | _reschedule_|
|              | General 2       | powersource |
|              | General 3       |             |

### Course 1: Mesh Workshop Updates
#### Objectives
- Workshop dev updates over the holidays
- Retrospective of our inaugural [Facilitating Mesh Workshops](https://tomesh.net/2018-12-17/facilitating-mesh-workshops/) event
- Ben is visiting Athens for a week end of month and exploring opportunities to connect with MaZi and mesh communities there
#### Links
- https://tomeshnet.github.io/p2p-internet-workshop/
- https://github.com/benhylau/mesh-router-builder
- https://tomesh.net/2018-12-17/facilitating-mesh-workshops/
- https://www.mazizone.eu
- https://netcommons.eu

### Course 2: Regulation Discussions in Course?
#### Objectives
- Is there a place in Course or general for discussion of regulations?

### Course 3: Debian Repository for Mesh Assets
#### Objectives
- Discuss the creation of a new debian repository for hosting of mesh/dweb related packages
- possible usage
    - replace prototype node module for cleaner install
    - place for mesh-orange to pull modules from
    - way of users to install individual modules without using full prototype node
- Evolution of prototype modules into deb packages
- Supported Arch -  arm/arm64/x86/x64
#### Links
- https://github.com/tomeshnet/mesh-services/issues/8

### General 2: Nordics and Nigeria
#### Objectives
- Talking about what's happening in the nordics and Nigeria

## Meeting notes

### General notes

- We are starting off having everyone add their name to the list of attendees
- Intros:
    - benhylau: organizes mesh syncs, with tomesh, workshops and infra
    - tim: engineering background, in ssb
    - yurko: tomesh, infrastructure set up
    - sgo: met ben at dimsumlabs, open-source, ip stack, programmer, oslo
    - zenna: denmark, zelf on ssb, meshnet implication, project side not technical, with Andre + Jacob et el. working on Nigeria project
    - jacob: computer science, working on project in Nigeria

### Course 1: Mesh Workshop Updates

- Gave updates on tomesh mesh workshop over the holidays
- Added Travis CI to build artifacts into GitHub Releases
- Added script to configure each node
- Added to workshop guide how to set up the software using a Raspberry Pi 3B or 3B+
- benhylau live demos how fast it is to set up (approximately 5 min) following [this guide](https://tomeshnet.github.io/p2p-internet-workshop/)
- yurko comments mesh-orange image is only 60 MB because it uses FAT as the files system. It does not need to "write" the part of the partition that has no files on it unlike ext2 or ext3
- Mentioned we held first [workshop for facilitators](https://tomesh.net/2018-12-17/facilitating-mesh-workshops/) in December

### Course 2: Regulation Discussions in Course?

- Pedro has been looking into Canadian regulations, notes added to [here](https://cryptpad.fr/code/#/2/code/edit/5sOZFsLkPPnEVRZFxSE7EW1b/)
- Met person who is interested in openning up cell phone wireless
- Frequencies and spectrum
- Study of regulations in Canada and around the world
- Regulations are written to broadcast, not necessarily from mesh
    - e.g. in Canada, broadcast publicly on frequencies require licenses, how about WiFi?
    - CRTC may be stricter on enforcement compared to US
    - Getting on the roof of public buildings require licenses
- Use benefits of p2p and make a case for opening dicussions of regulators
- tim: come up with a use case!
    - e.g. Hyperlocal newspaper + info at a sports event
    - Start with use case to recognize what regulations are in the way
- Building local politics is annoying
- Organization not legally bound
    - e.g. benhylau: deployment teams can be unrelated to organization that runs supernodes (add resiliency to network)

### Course 3: Debian Repository for Mesh Assets

- Group Debian packages to central repository
- [Prototype](https://github.com/tomeshnet/prototype-cjdns-pi) getting out of hand, too many modules
- How do we host one?
- Someone suggested gh-pages?
- Debian will allow us to support multiple archs with a sane structure
- Run it as [Mesh Service](https://github.com/tomeshnet/mesh-services/) (i.e. scripted deploy over Internet + mesh):
    - Digital Ocean is not available in some developing communities
    - Take things off the Internet
    - Digital Ocean as first target, then:
        - KVM + Proxmox
        - VirtualBox
        - NixOps
        - OVF

### General 2: Nordics and Nigeria

- Local knowledge in Scandanavia
- Test running SSB locally
- Zenna + Jacob + Alex
- At 35c3, met someone from Nigeria (rural) living in Copenhagen
- Andre Staltz also thinking mesh net for Manyverse
- LibreMesh experimentation
- Applying for project funding together! yay
- benhylau: cjdns/yggdrasil networks make offline applications easy
- yurko: Raspberry Pi + LibreRouter
    - Raspberry Pi to do processing
    - LibreRouter to do long-range WiFi radios
- yurko: [espressoBIN](http://espressobin.net) can be a lower cost device that combines Raspberry Pi processing power + a single WiFi radio from the LibreRouter
- benhylau to write post on SSB about radios and these two setups
    - _Update: Notes on this added to Zenna's meeting note thread on SSB `%/RQzQfHSX/qkrX8mXtL8TmheAjKQrQmNCXVVyNPamcM=.sha256`_
