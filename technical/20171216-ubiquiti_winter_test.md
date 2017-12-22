---
title: Ubiquity Winter Test
attendees: 1
date: 2017-12-16
---
# Ubiquity Winter Test
The test was to place a short term perminent node link between two balconies through the cold winter season. Test the resiliance of the node in the winter, and gather data.

## Deployment - 12/16/2017

Two TOMesh Ubiquity LiteBeam 5AC 23A Antennas where placed on to balconies with direct line of sight between them.

![NodeMap](../images/20171216-ubiquiti_winter_test_map1.png?raw=true)

The distance between the two nodes as approximatly 375 meters. At that distance the antennas are almost not visible.This made pointing the antennas a bit of a guessing game.  A signal lick of about -40dBm was established

![NodeMap](../images/20171216-ubiquiti_winter_test_distance.png?raw=true)

![NodeMap](../images/20171216-ubiquiti_winter_test_view.png?raw=true)

### RIG

The antennas where mounted on a ABS pipe stuck to a cinder block for support.


![NodeMap](../images/20171216-ubiquiti_winter_test_node1.png?raw=true)
![NodeMap](../images/20171216-ubiquiti_winter_test_node2.png?raw=true)

Each antenna had an  ORANGE PI ZERO with a 5ghz TSOP mesh antenna as a companion CJDNS device. These devices were connected together via Etherent Cable

The Ubiqity was set to PTP with network set to Bridge mode.

On the far end of the link, the  Orange Pi, and POE connector where placed inside the unit with the flat ethernet cable sliding under the balcony weather stripping and door while the antenna was left outside.

The other side, the Orange Pi was placed in a dollar store tupperware container plugged into outside power outlets.  The cables came out the bottom of the container and the container was tapped shut and with  the openning angled downward.

![NodeMap](../images/20171216-ubiquiti_winter_test_weather_proof.png?raw=true)

The near side node meshed over wifi and cjdns to the node located indoors.  That node in turn meshed with the Internet Enabled Atom computer with wifi capabilities. This provided a path to hyperborea and the internet.

![NodeMap](../images/20171216-ubiquiti_winter_test_map2.png?raw=true)

### Test
First tests - 
```
Cleanr ipv4
[ ID] Interval           Transfer     Bandwidth       Retr
[  4]   0.00-60.00  sec   661 MBytes  92.5 Mbits/sec  106             sender
[  4]   0.00-60.00  sec   661 MBytes  92.4 Mbits/sec                  receiver
CJDNS
 [ ID] Interval           Transfer     Bandwidth       Retr
[  4]   0.00-10.00  sec  61.1 MBytes  51.3 Mbits/sec   94             sender
[  4]   0.00-10.00  sec  60.5 MBytes  50.7 Mbits/sec                  receiver
```
Signal Strenght ~ 40 dBm


## Things Learned

* Both Ubiquity antennas where set to the same lan ip address of 192.168.1.20, this created an ip conflict on the bridged interface. One was changed to 192.168.1.21

* A bad power brick for the orange pi would prevent the WIFI and MESHPOINT from working. Rebooting would bring it up for a very short period of time

* So far the outdoor node preformed fairly well with outside temp dropping to -10 but node core temp not dropping below +8

* ABS Tube is not very ridgid and bend with the went fairly easly making the antenna sway slightly in windy conditions

* wireless throught a balcony door and screen has a decent signal strength but horrible throughput... After testing it could be the outside node

## Performance Deterioration test

```
[  4] local fc5e:44cd:6af4:4afc:cc4e:a75c:89a5:8d23 port 48622 connected to fc04:8b29:9889:cf83:88c:80fc:9e3b:78b4 port 5201
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  4]   0.00-1.00   sec   244 KBytes  2.00 Mbits/sec   12   13.2 KBytes
....
[  4]  58.00-59.00  sec   125 KBytes  1.02 Mbits/sec    1   21.7 KBytes
[  4]  59.00-60.00  sec   250 KBytes  2.05 Mbits/sec    1   20.5 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  4]   0.00-60.00  sec  9.12 MBytes  1.28 Mbits/sec  252             sender
[  4]   0.00-60.00  sec  8.98 MBytes  1.26 Mbits/sec                  receiver
```

### Analyisis
* Found that slowdown between outside node and 1st inside node
* Replaced inside node with new node and tplink adapter, no improvemnt
* Moved inside node outside, no improvement
* Moved node inside - VERY slight improvement (3-4 mbps)
* Took off top of tupper ware container - no improvemeet

```
[ ID] Interval           Transfer     Bandwidth       Retr
[  4]   0.00-10.00  sec  6.42 MBytes  5.38 Mbits/sec   56             sender
[  4]   0.00-10.00  sec  6.41 MBytes  5.38 Mbits/sec                  receiver
```

Signal strenght durring this whole time has been over -55 dBm
Confirmed speed test against differnt node slightly farther, speeds where 15Mbps, 

#### Testing
Possible Cause - bad radio
* Replaced usb radio with new module
* Issue seems to remains

Possible Cause - Bad power brick
* Replaced power brick
* Issue seems to remains

DRASTIC CHANGE
* One of the "inside nodes"
* low profile Small Case ( no fan )
* TPLink instead of TSOP usb wifi adapter
* Kept SD Card to preserv settings
* Issue Remains

## Modification - 12/20/2017
The orange pi node was moved inside, link quality improved. Metrics now recording correctly


## Bench Test - 12/20/2017

Further testing of nodes found that there may be an issues with the 3d pritned casing. when hardware is OUT of the case the speed is near 30mbps, placing it back in the case the speed drops to 5mbps

Further testing needed


