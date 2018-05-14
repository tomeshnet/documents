---
title: tomesh Tech Status Update
location: Toronto
date: 2018-05-11
---

# Overview

This document is a general overview of the technical pieces associate with Toronto Mesh as of May 2018. It includes general directions, key technical decisions, recent developments, and near-term roadmaps.

This is a good starting point to understand the current state of Toronto Mesh, what each technical project is building towards, and how the pieces fit together.

## Guiding Principles

We want a long-term sustainable mesh network with minimal need for centralized governance. Here are some features we feel are important:

* Self-determination of radio link arrangements
  * Physical and link layer decisions should be made between you and your immediate peers, whether the link uses _IBSS Ad-hoc_ or _802.11s Mesh Point_ at some frequency and SSID, or proprietary protocols like _Ubiquiti AirMAX_
  * Radio links are treated as "dumb pipes" that carry traffic of any mesh protocol indiscriminantly
  * Owners are free to apply any traffic control policy on their own radios

* Flexibility to run different mesh routing protocols
  * Traditional mesh software on routers (e.g. LibreMesh, Gluon, 🦇s)
  * Incentivized Internet sharing on routers (e.g. Althea)
  * Near-zero-configuration encrypted mesh on single-board computers, or SBCs (e.g. cjdns, yggdrasil)

* Localized and modular upgrades
  * You can never get an entire mesh to upgrade together, so hardware upgrades should be local decisions between you and your peer
  * You should be able to do modular hardware upgrades, for example, to change a SBC and keep all radio links
  * Reflect the reality that both hardware and software advance quickly, we need to be future-proof by letting people make upgrade decisions themselves than try to come to some global consensus about hardware or protocols that will never please everyone

## Mesh Node Architecture

### Radio Systems

Toronto Mesh is currently pursuing a couple opportunities to install this radio system on building rooftops near Dufferin and Queen. This effort is mostly led by [@Pedro-on-a-bike](https://github.com/Pedro-on-a-bike) and [@darkdrgn2k](https://github.com/darkdrgn2k).

```
+-------------+
| Radio with  |
| directional |
| antenna     |
+--------+----+
         |                 [more radios]
         |                       |
+--------+-----------------------+--------------------+
| 5-port Managed PoE Switch                           |
| VLAN tag packets from each antenna differently      |
+-----------------------------------------------------+
```

**Tested Products:**

* Ubiquiti LiteBeam AC 16 dBi running AirOS _CAD 110_
  * Configured as AirMAX Access Point, capable of both P2P and P2MP

* Ubiquiti Nanostation AC running AirOS _CAD 60_
  * Configured as AirMAX Station, connects to an AirMAX Access Point

* Ubiquiti TOUGH Switch PoE _CAD 120_
  * 24 V passive PoE to power most radio products
  * Managed gigabit switch to [isolate antenna traffic via VLANs](https://github.com/tomeshnet/mesh-isp/issues/2)

#### Ubiquiti Sector Radios

Building upon earlier tests on the Ubiquiti LiteBeam AC 23 dBi from [October 2016](https://github.com/tomeshnet/documents/blob/master/technical/20161015_gigabit-link-field-test.md) and [December 2017](https://github.com/tomeshnet/documents/blob/master/technical/20171216_ubiquiti-winter-test.md), [@Pedro-on-a-bike](https://github.com/Pedro-on-a-bike) has started constructing non-penetrating mounts and tested multiple _Ubiquiti Nanostation AC_ AirMAX Stations linking to a single _Ubiquiti LiteBeam AC 16 dBi_ AirMAX Access Point to exchange traffic concurrently.

![Ubiquiti Sector Radios](../images/20180511_tomesh-tech-status-update.jpg?raw=true)

### Mesh Routers

Radios connect two nodes and allow for single-hop traffic. In order to _mesh_, we need _mesh routers_ to direct traffic across multiple hops.

```
+-------------+
| Radio with  |
| directional |
| antenna     |
+--------+----+
         |                 [more radios]
         |                       |
+--------+-----------------------+--------------------+
| 5-port Managed PoE Switch                           |
| VLAN tag packets from each antenna differently      |
+------+----------------+-------------------+---------+
       |                |                   |
   (Internet)        (cjdns)        (cjdns & yggdrasil)
       |                |                   |
+------+------+ +-------+--------+ +--------+---------+
| EdgeRouterX | | Raspberry Pi 3 | | Orange Pi Zero   |
| with Althea | | with Prototype | | with Mesh Orange |
+-+-----------+ +-------+--------+ +--------+---------+
  |                     =                   =
  |                    ===                 ===
+-+-------------+     =====               =====
| Home Router   |
| Internet WiFi |  WiFi to cjdns & yggdrasil Networks
+---------------+
```

**Tested Products:**

* Ubiquiti EdgeRouterX _CAD 70_
* Raspberry Pi 3 _CAD 60_
* Orange Pi Zero _CAD 20_

#### Althea Deployment

![Mesh Network](../images/20180511_tomesh-tech-status-update2.png?raw=true)

* [Althea](https://altheamesh.com) nodes create a mesh network to access the Internet via _exit nodes_
* Includes cost metric to available routes and use microtransactions to incentivize people to put up nodes and sell bandwidth
* Lowers the barrier to start selling bandwidth (i.e. becoming an ISP, thus making the marketplace competitive)
* Runs on off-the-shelf routers running OpenWrt
* Uses a modified Babel protocol to mesh, cryptoeconomics experimental
* [@Pedro-on-a-bike](https://github.com/Pedro-on-a-bike) is leading a Toronto deployment

#### Mesh Networking with SBCs

![Content Mesh Network](../images/20180511_tomesh-tech-status-update3.png?raw=true)

* Brings the web content to the local mesh network, stored and accessed via peer-to-peer protocols and applications (e.g. IPFS, SSB)
* Addresses issues associated with _data aggregation_ (e.g. massive data breaches, state censorships) and our Internet _walled gardens_ (e.g. Google, Facebook)
* Runs on SBCs running Raspbian, Armbian, or Mesh Orange (off-the-shelf routers are unsuitable because they have insufficient processor power required by the applications)
* Uses [cjdns](https://github.com/cjdelisle/cjdns) or [yggdrasil](https://github.com/yggdrasil-network/yggdrasil-go) to route, forming encrypted near-zero-configuration networks with cryptographically allocated IPv6 addresses, but they are CPU intensive and routing over lossy radio links is work-in-progress
* [@darkdrgn2k](https://github.com/darkdrgn2k) and [@benhylau](https://github.com/benhylau) are leading development of _Prototype_ and [@hamishcoleman](https://github.com/hamishcoleman) for _Mesh Orange_

[Prototype](https://github.com/tomeshnet/prototype-cjdns-pi) is an installation script that runs on an existing _Raspbian_ or _Armbian_ operating system. We recently release [v0.2](https://github.com/tomeshnet/prototype-cjdns-pi/releases/tag/v0.2) with the following major features:

* Added support for Raspberry Pi 3 Model B+, EspressoBin, Rock64, NanoPi Neo 2, and many Orange Pi boards
* Added support to mesh using IBSS ad-hoc
* Added 802.11s mesh point RSSI threshold of -65 dBm to avoid routing over lossy links
* Added support for Internet gateway using cjdns iptunnel
* Improved node-exporter reporting to include cjdns information
* Added hostname renaming after running installation
* Added basic firewall
* Added hardware watchdog

[Mesh Orange](https://github.com/tomeshnet/mesh-orange) is a Debian-based minimal operating system that is in its early stage, but is designed to be reliable and upgradable for production environments. We have full control over the [build environment](https://github.com/benhylau/mesh-router-builder) and its architecture make it flexible for configuring network interfaces, switching mesh routing protocols, and running peer-to-peer applications:

```
+----------------+
| Docker p2papps | <- pull from repository with Dockerfiles of p2p apps built into docker images
+----------------+
| Mesh protocols | <- use mesh-router-builder Vagrant to build new .deb package and add to .img
+----------------+
| Network ifaces | <- add filter rules in mesh-orange conf.d/ to map driver to WiFi mode/config
+----------------+
| SBC boot dt fs | <- new mesh-orange build target to support new SBC, device tree, filesystem setups
+----------------+
```

In the last quarter, this OS and its toolchain have matured for us to design the [Peer-to-Peer Internet workshop](https://github.com/tomeshnet/p2p-internet-workshop/) around a custom build of its image.

Here is a comparison between our two main software projects:

|               | Prototype                   | Mesh Orange                 |
|:--------------|:----------------------------|:----------------------------|
| OS            | Raspbian or Armbian         | Mesh Orange (Debian-based)  |
| OS image size | 250 - 350 MB                | 50 - 100 MB                 |
| Installation  | 10 min, requires Internet   | 1 min, self-contained image |
| Development   | Writing bash scripts        | Building OSs for ARM boards |
| Use case      | New devices and prototyping | Reproducible & reliable     |

>_"But that's a CAD 500 mesh node?!"_ — `(╯°□°）╯︵ ┻━┻`

## SBC Mesh Router

![SBC Mesh Node](../images/20180511_tomesh-tech-status-update4.jpg?raw=true)

While USB WiFi dongles (e.g. [TOP-GS07](https://github.com/tomeshnet/documents/blob/master/technical/20170208_mesh-point-with-topgs07-rt5572.md)) have served us very well forming 802.11s mesh links in a small areas, these radio devices have limited range, bandwidth, and sometimes stability issues. [LibreRouter](https://librerouter.org) has already been tackling the issue with finding low-cost mesh-friendly directional radios with Linux-friendly drivers, our plan is to take their radio + antenna package and put that on a SBC with mPCIe interfaces, such as:

* [ESPRESSObin](http://espressobin.net) _CAD 70_
* [ClearFog Pro](https://www.solid-run.com/marvell-armada-family/clearfog/) _CAD 250_
* [ClearFog GT 8K](https://www.solid-run.com/marvell-armada-family/clearfog-gt-8k/) _CAD 400_

Unfortunately choices are quite limited for SBCs with powerful CPUs that also have extensive networking interfaces (i.e. many gigabit ethernet ports and 2+ mPCIe slots), but we hope with time cost will come down to < CAD 100 for the full device, complete with directional antennas and running Mesh Orange. The [original Mesh Orange hardware plan](https://github.com/tomeshnet/mesh-orange/issues/1) is a precursor to this project and that was for a USD 20 mesh node.

## Peer-to-peer Applications

Some of the first questions after setting up our Prototype nodes were _"what can we do with this?"_ They do not connect to the Internet by default, so what can we do aside from pings and speed tests?

### Live Video Streaming on IPFS

We have the distributed file store _Interplanetary File System (IPFS)_ running on both Prototype and Mesh Orange, and [@ASoTNetworks](https://github.com/ASoTNetworks) and [@darkdrgn2k](https://github.com/darkdrgn2k) have gotten _HTTP Live Streaming (HLS)_ to work over IPFS. They are leading the project to live stream [Our Networks 2018](http://ournetworks.ca) conference this July.

### Decentralized Social Networking with Secure Scuttlebutt

Now that we have IPFS running on Mesh Orange in a docker container, we want to do the same for many peer-to-peer applications. [@benhylau](https://github.com/benhylau) and [@darkdrgn2k](https://github.com/darkdrgn2k) are working to get _Secure Scuttlebutt (SSB)_ running on the SBCs and part of the workshop series. This could be a major use case that rely only on in-mesh traffic. This work is supported by a [grant by the Secure Scuttlebutt Consortium](https://github.com/benhylau/ssbc-grants-scuttlemesh).

## Mapping & Monitoring

Our mesh nodes voluntarily report metrics using [Node Exporter](https://github.com/prometheus/node_exporter) and monitors use [Prometheus](https://prometheus.io) to poll for these metrics across the network. [Grafana](https://grafana.com) is used to display the data points graphically:

![Mesh Node Monitoring](../images/20180511_tomesh-tech-status-update5.png?raw=true)

Node location data is pulled from our [Node List](https://github.com/tomeshnet/node-list/) and plotted on our [Node Map](https://tomesh.net/map/), with updated themes by [@Shrinks99](https://github.com/Shrinks99):

![Mesh Node Mapping](../images/20180511_tomesh-tech-status-update6.png?raw=true)

Over the last couple months, [@darkdrgn2k](https://github.com/darkdrgn2k) has made significant progress with mapping the [physical network](http://node2.e-mesh.net:4000/map/) and [logical network](http://node2.e-mesh.net/vis/) with real-time data, as well as [configuring the Grafana dashboards](http://node2.e-mesh.net:3000/dashboard/db/mesh-node-metrics-fixed). The code exists as various scripts not currently deployed to the Toronto Mesh website, and the work necessary to "productize" these shiny real-time features are tracked on [tomeshnet/tomesh.net](https://github.com/tomeshnet/tomesh.net/issues):

* [Live Map Status](https://github.com/tomeshnet/tomesh.net/issues/211)
* [Add Node Workflow](https://github.com/tomeshnet/tomesh.net/issues/207)

This is quite a significant amount of work, but once completed the entire _Mapping & Monitoring_ system can be reusable for other cjdns-based mesh communities. If you are interested in taking on this work, find us at [#monitoring:tomesh.net](https://chat.tomesh.net/#/room/#monitoring:tomesh.net).
