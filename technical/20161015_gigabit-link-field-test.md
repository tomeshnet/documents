---
title: Gigabit Link Field Test
location: Tommy Thompson Park
attendees: 10
date: 2016-10-15
startTime: 09:00
endTime: 15:00
---

# Test Setup & Objectives

A pair of Ubiquiti LiteBeam ac each powered by a ChargeTech 27 Ah portable battery through the PoE injector that the radios ship with. The LAN port of the injector is connected through an ethernet cable to an Ethernet-to-Thunderbolt gigabit adapter to a Mac. These two fully portable setups are largely symmetric. The LiteBeam ac's run AirOS and the Mac's run OS X with cjdns and other networking tools installed. On one of the ChargeTech batteries, we have attached a Kill-a-watt to measure the power draw of the LiteBeam ac units while idling and transmitting.

The objective of this exercise is to determine feasibility of using the LiteBeam ac to establish point-to-point, or perhaps point-to-multipoint, links for tomesh. We are primarily interested in the bandwidth and range performance of the unit, and secondary to that: power requirements, ease of set up, effects on obstructions by different objects in its line-of-sight path, and compatibility with cjdns.

On an early Saturday morning, the group met at a coffee shop near Tommy Thompson Park, where there is a somewhat straight section of a few kilometres of flat land, which unfortunately does not have elevated points, but is a reasonable site for this first test. There we powered up the LiteBeams for the very first time.

# Initial Findings

- The Mac clients need to manually assign an IP to itself, with the router IP at its default **192.168.1.20**
- Connect with the AirOS web interface at **http://192.168.1.20**
- Switching one of the LiteBeams to **Router Mode** from the default **Bridge Mode** made it impossible to connect to again, this is probably due to our general infamiliarity with AirOS, but we had to reset that LiteBeam, and the reset button was damn hard to reach
- One LiteBeam was in **Station Mode** and the other in **Client Mode**, I don't recall if that was reverted and not reconfigured after the reset
- We changed one LiteBeam's IP to **192.168.1.19**, and once the link is established, only one of the two IPs become reachable from the Macs
- We initially had trouble having the Macs (each with a unique IP in the **192.168.1.0/24** subnet)  ping each other over the LiteBeam link, but eventually that started working after the resets and assigning different IPs to each LiteBeam
- Using `iperf3` while the LiteBeams were sitting right beside each other, the link was about 370 Mbps
- We expected cjdns running on the Mac to automatically bind to the point-to-point interface and automatically establish autopeering over the cjdns `ETHInterface`, but that didn't happen, neither did AirOS show cjdns' `tun0` as an interface
- We manually forced cjdns to bind to the point-to-point interface by changing `"bind": "all"` to `"bind": "x"`, where _x_ is `en3` on one Mac and `en5` which we found from `ifconfig`, after that the two Mac nodes autopeered over ethernet and we are able to ping each other through their cjdns addresses
- The cjdns link `iperf3` at only 20 Mbps, which remains a mystery because the underlying link is 370 Mbps, and I have seen these Macs do at least 50 Mbps through the `UDPInterface`, limited only by my home Internet speeds, and based on `cjdroute --bench` results I'd expect the Macs to saturate the raw link
- Since we are primarily interested in the LiteBeam performance over distance, this is when we moved on to Tommy Thompson Park

# Range Testing

We had one group mount a LiteBeam at about 8 ft on a pole at (43.645771, -79.320951), while the other group moved away from it and stopped at various distances.

## Test Point A, 227 m away at (43.643781,-79.321583)

```
$ ping 192.168.1.25
PING 192.168.1.25 (192.168.1.25): 56 data bytes
64 bytes from 192.168.1.25: icmp_seq=0 ttl=64 time=1.263 ms
64 bytes from 192.168.1.25: icmp_seq=1 ttl=64 time=1.363 ms
64 bytes from 192.168.1.25: icmp_seq=2 ttl=64 time=2.432 ms
64 bytes from 192.168.1.25: icmp_seq=3 ttl=64 time=2.972 ms
64 bytes from 192.168.1.25: icmp_seq=4 ttl=64 time=1.273 ms
64 bytes from 192.168.1.25: icmp_seq=5 ttl=64 time=1.322 ms
64 bytes from 192.168.1.25: icmp_seq=6 ttl=64 time=1.345 ms
64 bytes from 192.168.1.25: icmp_seq=7 ttl=64 time=2.797 ms
^C
--- 192.168.1.25 ping statistics ---
8 packets transmitted, 8 packets received, 0.0% packet loss
```

```
$ iperf3 -c 192.168.1.25
Connecting to host 192.168.1.25, port 5201
[  4] local 192.168.1.21 port 51076 connected to 192.168.1.25 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec  45.2 MBytes   379 Mbits/sec
[  4]   1.00-2.00   sec  45.1 MBytes   378 Mbits/sec
[  4]   2.00-3.00   sec  42.4 MBytes   355 Mbits/sec
[  4]   3.00-4.00   sec  43.9 MBytes   368 Mbits/sec
[  4]   4.00-5.00   sec  41.2 MBytes   346 Mbits/sec
[  4]   5.00-6.00   sec  41.0 MBytes   343 Mbits/sec
[  4]   6.00-7.00   sec  44.6 MBytes   374 Mbits/sec
[  4]   7.00-8.00   sec  43.7 MBytes   366 Mbits/sec
[  4]   8.00-9.00   sec  44.3 MBytes   371 Mbits/sec
[  4]   9.00-10.00  sec  42.4 MBytes   356 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec   434 MBytes   364 Mbits/sec                  sender
[  4]   0.00-10.00  sec   434 MBytes   364 Mbits/sec                  receiver
```

**Obstruction one foot in front of one LiteBeam:**

```
$ iperf3 -c 192.168.1.25
Connecting to host 192.168.1.25, port 5201
[  4] local 192.168.1.21 port 51170 connected to 192.168.1.25 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec  44.1 MBytes   370 Mbits/sec
[  4]   1.00-2.00   sec  39.4 MBytes   329 Mbits/sec
[  4]   2.00-3.00   sec  9.90 MBytes  83.4 Mbits/sec
[  4]   3.00-4.00   sec  37.0 MBytes   310 Mbits/sec
[  4]   4.00-5.00   sec  41.6 MBytes   349 Mbits/sec
[  4]   5.00-6.00   sec  34.1 MBytes   286 Mbits/sec
[  4]   6.00-7.01   sec  7.67 MBytes  64.0 Mbits/sec
[  4]   7.01-8.00   sec  29.3 MBytes   247 Mbits/sec
[  4]   8.00-9.00   sec  15.9 MBytes   133 Mbits/sec
[  4]   9.00-10.00  sec  34.9 MBytes   293 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec   294 MBytes   246 Mbits/sec                  sender
[  4]   0.00-10.00  sec   293 MBytes   246 Mbits/sec                  receiver
```

**Over cjdns:**

```
$ iperf3 -c fcfd:cce:14ab:57de:64f7:32e3:19f3:ebdf
Connecting to host fcfd:cce:14ab:57de:64f7:32e3:19f3:ebdf, port 5201
[  4] local fcaf:c9e1:bfff:73a3:c08c:51aa:3711:2ccc port 51316 connected to fcfd:cce:14ab:57de:64f7:32e3:19f3:ebdf port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.01   sec  2.49 MBytes  20.8 Mbits/sec
[  4]   1.01-2.00   sec  2.04 MBytes  17.2 Mbits/sec
[  4]   2.00-3.00   sec  2.68 MBytes  22.5 Mbits/sec
[  4]   3.00-4.01   sec  1.41 MBytes  11.8 Mbits/sec
[  4]   4.01-5.00   sec  2.58 MBytes  21.8 Mbits/sec
[  4]   5.00-6.00   sec  3.12 MBytes  26.2 Mbits/sec
[  4]   6.00-7.00   sec  3.06 MBytes  25.7 Mbits/sec
[  4]   7.00-8.00   sec  3.01 MBytes  25.3 Mbits/sec
[  4]   8.00-9.00   sec  3.10 MBytes  26.0 Mbits/sec
[  4]   9.00-10.00  sec  3.37 MBytes  28.3 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec  26.9 MBytes  22.5 Mbits/sec                  sender
[  4]   0.00-10.00  sec  26.7 MBytes  22.4 Mbits/sec                  receiver
```

**Notes:**

- If we introduced a misalignment of about 20 degrees, speed drops to < 100 mbps
- There were points when we had to restart `cjdroute` for things to work

## Test Point B, 596 m away at (43.641396, -79.322121)

```
$ iperf3 -c 192.168.1.22
Connecting to host 192.168.1.22, port 5201
[  4] local 192.168.1.21 port 53527 connected to 192.168.1.22 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec  43.5 MBytes   365 Mbits/sec
[  4]   1.00-2.00   sec  47.2 MBytes   395 Mbits/sec
[  4]   2.00-3.00   sec  45.3 MBytes   380 Mbits/sec
[  4]   3.00-4.00   sec  45.8 MBytes   384 Mbits/sec
[  4]   4.00-5.00   sec  44.5 MBytes   373 Mbits/sec
[  4]   5.00-6.00   sec  45.3 MBytes   380 Mbits/sec
[  4]   6.00-7.00   sec  47.6 MBytes   399 Mbits/sec
[  4]   7.00-8.00   sec  47.5 MBytes   399 Mbits/sec
[  4]   8.00-9.00   sec  45.4 MBytes   381 Mbits/sec
[  4]   9.00-10.00  sec  45.9 MBytes   385 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec   458 MBytes   384 Mbits/sec                  sender
[  4]   0.00-10.00  sec   457 MBytes   384 Mbits/sec                  receiver
```

**180 degree offset (lol wut? bc we can):**

```
$ iperf3 -c 192.168.1.22
Connecting to host 192.168.1.22, port 5201
[  4] local 192.168.1.21 port 53533 connected to 192.168.1.22 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec  9.66 MBytes  81.0 Mbits/sec
[  4]   1.00-2.00   sec  10.9 MBytes  91.9 Mbits/sec
[  4]   2.00-3.00   sec  9.76 MBytes  81.9 Mbits/sec
[  4]   3.00-4.00   sec  8.12 MBytes  68.2 Mbits/sec
[  4]   4.00-5.00   sec  7.92 MBytes  66.4 Mbits/sec
[  4]   5.00-6.00   sec  8.79 MBytes  73.8 Mbits/sec
[  4]   6.00-7.01   sec  5.63 MBytes  47.0 Mbits/sec
[  4]   7.01-8.00   sec  8.05 MBytes  67.9 Mbits/sec
[  4]   8.00-9.00   sec  7.90 MBytes  66.1 Mbits/sec
[  4]   9.00-10.00  sec  4.96 MBytes  41.7 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec  81.7 MBytes  68.6 Mbits/sec                  sender
[  4]   0.00-10.00  sec  81.7 MBytes  68.6 Mbits/sec                  receiver
```

## Test Point C, 863 m away at (43.638118, -79.322729)

- No line-of-sight, blocked by a bunch of trees, Fresnel zone probably cuts deep into the ground because the antennas are at ground level
- A few kbps intermittenly, signal dropping all the time
- Tried changing polarization but that made no difference
- AirOS web interface on one site does not load, consistent with our belief that once linked, only one LiteBeam is routing while the other one is just bridging
