---
title: Cantenna Field Test
location: Bridge along Bathurst above the train tracks, 9 Bathurst St
attendees: 7
date: 2017-03-11
startTime: 09:00
endTime: 13:00
---

# Cantenna Field Test

A pair of 2.4 GHz cantennas and pigtail cables were made following these resources:

- [How Cantenna Works?](https://propakistani.pk/2010/03/19/how-cantenna-works-technically/)
- [Coffee Can Antenna](http://www.binarywolf.com/249/coffee_can_antenna.htm)
- [Wireless 2.4 GHz Directional Antenna Calculator](http://www.csgnetwork.com/antennawncalc.html)

They were tested at [this event](https://tomesh.net/2017-03-11/cantenna-field-test/). Here are the results of our tests and photos of our setups and their making of.

## Making Of Cantenna

### Parts

![Parts](../images/20170311_cantenna-field-test.jpg?raw=true)

Note that the adapters we used for the field test are **TL-WN722N** instead.

### RP-SMA to N-type Pigtail Cable

![Pigtail 1](../images/20170311_cantenna-field-test2.jpg?raw=true)
![Pigtail 2](../images/20170311_cantenna-field-test3.jpg?raw=true)
![Pigtail 3](../images/20170311_cantenna-field-test4.jpg?raw=true)
![Pigtail 4](../images/20170311_cantenna-field-test5.jpg?raw=true)

You can also buy these pre-assembled, but I had trouble finding them locally at the time.

### Radiator and Cantenna

![Cantenna 1](../images/20170311_cantenna-field-test6.jpg?raw=true)
![Cantenna 2](../images/20170311_cantenna-field-test7.jpg?raw=true)
![Cantenna 3](../images/20170311_cantenna-field-test8.jpg?raw=true)

I used a regular drill bit to make the slot to insert the radiator, but a step bit would have been ideal for the job.

### Test Nodes

![Node 1](../images/20170311_cantenna-field-test9.jpg?raw=true)
![Node 2](../images/20170311_cantenna-field-test10.jpg?raw=true)

Each node is a Raspberry Pi 3 connected with a TL-WN722N powered with a portable battery pack. The SD card has Raspbian and [our mesh software](https://github.com/tomeshnet/prototype-cjdns-pi) installed, routing with cjdns over the Mesh Point interface. We basically have two of the nodes as pictured in the first photo, with the omnidirection antennas swapped for a cantenna, each on one bridge pointing to one another.

We later played with a yagi antenna, in the second photo, but did not test that over the bridge.

## Results

We primarily used [noping](https://noping.cc/) and `iperf3` over the cjdns interface (i.e. `tun0`) to plot pings and measure throughput, and `watch -d 'iw dev mesh0 station dump'` to monitor signal strength and expected throughput over the Mesh Point interface (i.e. `mesh0`).

When we had the cantennas beside each other, signal strength over `mesh0` was -30 dBm, pings were all delivered and network throughput above 20 Mbps over `tun0`. When we placed them across the 280 m distance between the two bridges, the Mesh Point peering picked up as soon as we roughly aimed the cantennas toward each other. The signal strength dropped to -85 dBm, roughly 20% of pings were dropped and network throughput dropped to 0.5 Mbps. The degraded network performance is consistent with [what we'd expect with the -85 dBm signal strength](https://support.metageek.com/hc/en-us/articles/201955754-Understanding-WiFi-Signal-Strength).

These homemade cantennas did not perform as well as I was hoping for. It's unclear whether it was flaws in the construction of the cantennas or pigtails, or perhaps the noise base in the area, or limitation of the design that made them unusable at 280 m. Another observation was when we tried to peer them across a glass window, that completely attenuated the signal even though the nodes were less than 20 feet apart. Further tests will be conducted in the future to determine the useful range.
