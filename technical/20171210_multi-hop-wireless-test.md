---
title: Multi Hop Wireless Test
location: Toronto Reference Library
attendees: 5
date: 2017-12-10
startTime: 13:30
endTime: 17:00
---

# Multi Hop Wireless Test at the Toronto Reference Library

The goal of the [TRL Mesh Test](https://www.tomesh.net/2017-12-10/trl-mesh-test/) was to test how well the current state of our mesh nodes and mesh software would perform in a multi hop environment when routing over wireless links.

Technologies tested include:

* Boards: Raspberry Pi 3, Orange Pi Zero
* Radios: TP-LINK TL-WN722N, Toplinkst TOP-GS07, Ubiquti LBE‑5AC‑23
* Link (Layer 1): 802.11s Mesh Point at 2.4 GHz without forwarding
* Mesh (Layer 2 and 3): cjdns for addressing and routing
* Monitoring: Custom reporting and graphing software prepared by @darkdrgn2k, various Linux tools

## Preparing The Nodes

Seven nodes were prepared using Raspberry Pi 3's and Orange Pi Zero's running the latest [prototype script at the time](https://github.com/tomeshnet/prototype-cjdns-pi/commit/0dcfd635fee5f0d280339957d515fb6a58d85827) with the following command:

```
$ wget https://raw.githubusercontent.com/tomeshnet/prototype-cjdns-pi/develop/scripts/install && chmod +x install && WITH_MESH_POINT=true WITH_WIFI_AP=true WITH_IPFS=false WITH_PROMETHEUS_NODE_EXPORTER=false WITH_PROMETHEUS_SERVER=false WITH_GRAFANA=false WITH_H_DNS=true WITH_H_NTP=true WITH_FAKE_HWCLOCK=false WITH_EXTRA_TOOLS=true TAG_PROTOTYPE_CJDNS_PI=develop ./install
```

Each node was then manually configured to also report metrics to a collection node on the LAN.

## Test Sessions

### Deploy All The Nodes

We deployed seven nodes on the 5th floor of the Toronto Reference Library (TRL). We separated them with a distance that would keep each node in fair communication with the next one, which is only a couple metres apart. Not all the nodes have line-of-sight with each other. The diagram shows the approximate node positions, and their signal strength from the control node on our work table at a single point in time.

![Node positions](../images/20171210_multi-hop-wireless-test.png?raw=true)

#### Monitoring Software

Our collection node collects metrics from the deployed nodes and generate graphs that tell us the self-forming topology of our mesh network. This is one graph showing the cjdns peerings among nodes:

![cjdns peerings](../images/20171210_multi-hop-wireless-test2.png?raw=true)

A second graph shows the MAC address of the Mesh Point device on each node, as well as the cjdns IPv6 address, linked by Mesh Point peerings with radio signal strengths reported by the interfaces:

![Mesh topology](../images/20171210_multi-hop-wireless-test3.png?raw=true)

The graphs are helpful in understanding how each node is seeing other nodes in the self-forming mesh network. We encountered two issues that were somewhat addressed during the test:

* Since some nodes have Internet connectivity and Hyperboria peers, we find nodes that appear on the graphs that are actually from the Internet and having no differentiation in the rendering made it difficult to interpret the graphs (we addressed that by blacklisting nodes in the rendering script during the test)
* In the second graph, you will find nodes that have a MAC address but no cjdns address, and we believe that's because the connections are so poor with some nodes that although they are peered over Mesh Point, the nodes were unable to deliver metrics to the collection server

In future tests we should continue to identify nodes by their cjdns IPv6 address, and map to their Mesh Point device MACs, so we can correlate radio metrics from `iw station dump` with IP traffic data such as ping drops and latency from both the raw and cjdns interface, route and hop information, iperf3 bandwidth, etc. It would also be useful to improve reliable delivery of the metrics to the collection node.

#### Network Performance

The network became almost completely unusable when trying to communicate with nodes further away. SSH sessions have huge latencies and even delivery of metrics to the collection server was unreliable.

* 802.11s Mesh Point by default will connect with any node it sees in it vicinity regardless of signal strength
* cjdns is configured to peer with each node over ETHInterface beacon at Layer 2
* cjdns routing looks for least-hop route and does not take link quality into consideration

This essentially makes the entire test network a 1-hop network :(

#### Theory & Example

![Parts](../images/20171210_multi-hop-wireless-test4.png?raw=true)

The connection from Node 1 to Node 4 is a direct connection even though the signal strength is a very low -70dBm. This result in a nearly unusable connection. A much cleaner connection would go from `Node 1 -> 2 -> 3 -> 4`, but because this would require more hops cjdns will _not_ take this path.

### Three-node Deployment

To try to recover from the roadblock and test a multi hop network, we attempted to create a simple three-node test. The goal was to place two nodes on opposite sides of the library so they could not communicate with each other. We would then place an intermediate node in between the two points to establish a 3 hop network.

### Results

We could not find a place in the library where the first two nodes were not visible to each other. They kept a connection even at the extremes, at an unusable signal strength of -90 dBm. This is consistent with earlier tests at across the bridges when we saw < 1 Mbps bandwidth, but Mesh Point peering was established with no difficulty.

## Next Steps

Thoughts after looking at the test results:

* Nodes retain information about old nodes they saw for a long period of time
* Nodes we saw listed under "station dump" may have been cached and not actually visible
* We should use `mesh plink: ESTAB` as a test to see if a node is actually peered

### Long-term Solution

Apart from the need for more reliable wireless hardware, for this mesh network to become usable, we need cjdns to deal more intelligently with deciding which path to take when met with multiple paths that include poor quality links. The solution needs to work with the design of cjdns being agnostic to the physical transport. For example, we have discussed whether we can have a generic way of measuring link quality, or have an interface through which the user may supply generic metrics through an implementation specific to the type of links in use.

### Possible Alternative

Another option would be to run a Layer 2 network under the cjdns protocol to make all nodes one hop away cjdns' perspective. This would prevent cjdns from routing poorly, leaving it to other protocols that take link quality into account.

Some suggestions were to add a TTL to the connection, however this may start conflicting with cjdns' routing implementation. The only way this will work is if isolated networks with a finite amount of "exit/enter" connections meshed at Layer 2 as a whole. This will limit the ping domain to the local area only, while cjdns still routes out to "the rest of the world".

### Immediate Solution

#### 802.11s Native Solution

After researching some of the options available in 802.11s, we found a configuration that will block new links to be formed if the signal strength is below a certain threshold. The following line was added to our mesh script after the fact to help mitigate the issue we found:

```
sudo iw dev $mesh_dev set mesh_param mesh_rssi_threshold -70
```

However, this solution will _not_ drop connections that fall below the threshold _after_ they are established. If the signal becomes lossy after initial peering, this setting will not address the problem.

#### "Signal Watcher" Solution

It would be possible to create a process that can "watch" the signal strength of all the peers and block connections below a threshold with:

```
iw dev $mesh_dev station set $mac plink_action block
```

then unblock the interface by MAC when signal strength rises above the threshold with:

```
iw dev $mesh_dev station set $mac plink_action open
```

The issue here is that it will take some time for cjdns to realize the path is no longer active and re-route on the local node. There is currently no way to force drop a specific cjdns peer, or even identify which peer uses which connection.

# Antenna Tests

While in a large space we tested antennas through the open area in the middle of the Toronto Reference Library.

## Yagi Antennas

Two 2.4 GHz Yagi antennas where purchased from eBay as a potential low-cost long distance link:

![Yagi antenna](../images/20171210_multi-hop-wireless-test5.jpg?raw=true)

We plugged in two TL-WN722N into two Raspberry Pi 3's and attached a Yagi to each one, then separated them across the void in TRL. The Yagi antennas did not work at all in the environment.  The signal strength across the void in the centre of the library was -90 dBm. It is suspected that the antenna used is of low quality.

There are many theory’s why the Yagi did not work:

* The device quality was poor
* The ambient 2.4 GHz traffic of the existing library WiFi created too much noise (Yagi's amplify noise)
* They were not far enough apart to work correctly
* They were not pin-point precision targeted
* They need a more powerful "PC card" to function and USB dongles do not provide enough power

## Ubiquiti LiteBeam ac (LBE‑5AC‑23)

The pair of LiteBeam devices were plugged into two Raspberry Pi 3's and positioned across the 5th floor. Then one took an elevator down to the basement and all the way maintained solid iperf3 performance and very little packet drop on ping. On both clear IP and cjdns bandwidth tests, the Raspberry Pi 3's capability (10/100 ethernet and CPU bottleneck for cjdns) are used to the limit. The wireless link performs excellent at these < 1 km distances even with misalignments and obstacle. The only significant drop in performance observed was when I pointed one antenna through a solid block of concrete from the library basement. On a board with gigabit ethernet and a faster CPU, we expect to see much higher speeds than 100 Mbps.