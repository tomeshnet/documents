---
title: Multi Hop Wireless Test and Antenna Test
attendees: 5
date: 2017-12-10
startTime: 13:30
endTime: 17:00
---

# TRL Multi Hop Wireless Test

Goal was to test how well the current state of our mesh nodes and mesh software would perform with a multi hops environment  routing over wireless networks.  

The tests where preformed at [this event](https://www.tomesh.net/2017-12-10/trl-mesh-test/)

Technologies tested where
* 802.11s without forwarding - layer 1 interconnect
* CJDNS - Layer 2 and 3 meshing software

## Preparing the nodes

7 Nodes where prepared using Orange Pi Zeros and Raspberry Pi using the latest prototype script [at the time](https://github.com/tomeshnet/prototype-cjdns-pi/commit/0dcfd635fee5f0d280339957d515fb6a58d85827) with the following command

```$ wget https://raw.githubusercontent.com/tomeshnet/prototype-cjdns-pi/develop/scripts/install && chmod +x install && WITH_MESH_POINT=true WITH_WIFI_AP=true WITH_IPFS=false WITH_PROMETHEUS_NODE_EXPORTER=false WITH_PROMETHEUS_SERVER=false WITH_GRAFANA=false WITH_H_DNS=true WITH_H_NTP=true WITH_FAKE_HWCLOCK=false WITH_EXTRA_TOOLS=true TAG_PROTOTYPE_CJDNS_PI=develop ./install```

## Multiple Node Deployment

We deployed 7 nodes at the 5th floor of the Toronto Reference Library (TRL). We separated them with a distance that would keep each node in fair communication with the next one. Not all the nodes where line of sight with each other.

The diagram shows the approximate node positions, and their signal strength from the control node on our work table at a single point in time.

![NodeMap](../images/20171210_wirless_multi_hop_map.png?raw=true)

### Results

We found that the network became almost completely unusable when trying to communicate with nodes further away. 

#### Analysis

* 802.11s by design will connect with any node it sees in it vicinity regardless of signal strength.
In turn CJDNS will peer to each node it finds on a given node.
CJDNS's routing will look for least-hops route and does not take link quality into effect.

#### Theory and example

![Parts](../images/20171210_wirless_multi_hop_issue_diagram.png?raw=true)

The connection from node 1 to node 4 is a direct connection even though the signal strenght is a very low -70dDm

This causes a nearly unusable connection.  A much cleaner conneciton would from node1-2-3-4, but because this would require more hops cjdns will NOT take this path.

## Deployment off 3 node test

To try to gain more insight into what is happening, we attempted to create a 3 node test. The goal was to place two nodes on opposite sides of the library so they could not communicate with each other. We would then place an intermediate node in between the two points to establish a 3 hop network.

### Results
We could not find a place in the library where the two nodes where not visible to each other. It kept a connection even at the extremes as an unusable signal strength of -90dBm.


## Long term Solution

The only way this would become usable is if CJDNS matures into being able to deal more inteligently with deciding which path to take when met with multiple paths and poor quality conditions.

## Possible alternative
Another option would be to run a layer 2 network under the CJDNS protocol to make all nodes 1 hop away in CJDNS's eyes.  This would prevent CJDNS from routing poorly leaving it to other protocols that take link quality into account.

## Immediate solution


### 802.11s Native solution
After researching some of the options available in 802.11s there is a configuration that will block new links to be formed if the signal is before a certain threshold. The following line was added to our mesh script after the fact to help mitigate the issue we found

```sudo iw dev $mesh_dev set mesh_param mesh_rssi_threshold -70```

This solution will NOT drop connections that fall bellow the threshold AFTER they are established.

### "Signal Watcher" Solution

It would be possible to create a process that can "watch" the signal strength of all the peers and block connections below a threshold with ```iw dev $mesh_dev station set $mac plink_action block``` and unblock them when they rise above the threshold with ```iw dev $mesh_dev station set $mac plink_action open```

One issue we face with this configuration is that it will take some time for CJDNS to find that the path is no longer active and reroute on the local node. There is currently no way to drop a specific peer or even identify which peer uses with connection. 


# Antenna Test

While in a large space we tested antennas through the open area in the middle of the TRL Library

## Yagi

The Yagi antenna was purchased from eBay as a possible and cheap long distance link. 

### Setup
We plugged in two TL-WN722N into two Raspberry Pi devices.  Attached a Yagi to each one and then separated them across the void in TRL.

### Results

The yagi antenna did not work at all in the environment.  The signal strength across a void in the center of the library was -90dBm.  It is suspected that the antenna used is of low quality.


### Analysis

There are many theory’s why the Yagi did not work

* They are Chinese quality devices
* The ambient 2.4ghz traffic of the existing WIFI created to much noise (Yagi's amplify noise)
* They where not far enough apart to work correctly
* They where not pin-point precision targeted
* They need a more powerful "pc card" to function and USB Dongles do not provide enough power

## Ubiquiti LiteBeam ac

### Setup
The Ubiquities where plug into two raspberry pi and positioned diagonally from the Basement floor to  5th floor.

### Results
The antenna preformed very well and maxed out the pi's capabilities.

