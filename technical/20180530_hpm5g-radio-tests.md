---
title: HPM5G Radio Tests
location: Toronto
attendees: 8
date: 2018-05-30
---

# Overview 

This document summarizes a series of tests on the **Dragino HPM5G mPCIe radio module** and the **LibreRouter's 12 dBi antenna** that are expected to ship with the soon-to-be-released LibreRouter bundle. Toronto Mesh acquired six radio boards and antennas from Dragino, and in this test, used a pair of the [Marvell ESPRESSObin](http://espressobin.net) running [prototype](https://github.com/tomeshnet/prototype-cjdns-pi) to test the radios.

![Dragino HPM5G mPCIe radio module](../images/20180530_hpm5g-radio-tests.jpg?raw=true)
![LibreRouter's 12 dBi antenna](../images/20180530_hpm5g-radio-tests2.jpg?raw=true)

## Issues

Using our ESPRESSObin setup, the HPM5G board was automatically identified and brought up on boot with the `ath9k` driver. Throughout testing, we observed a couple issues that we were able to work around.

### Power Issues on the ESPRESSObin mPCIe

During the initial setup and testing we noticed that the ESPRESSObin would restart at what seemed to be random times. We tried different combination of radio boards and ESPRESSObin boards but the issue was persistent. We tried to reach out to the ESPRESSObin community without any luck; however the Armbian community mentioned that this seemed like an issue with insufficient power. Identifying this as a potential power issue we tried using larger amperage power supplies (1.5 and 2 A at 12 V) however this did not seem to solve the problem.

**Work Around**

After identifying a potential power problem we tried to limit the amount of power the radio would need by reducing the TX power of the radio. We found that keeping it around 14 dBm would let the ESPRESSObin operate without reboot. Our initial testing was then done using a 14 dBm TX power.

We did run into an issue where the TX power would not be persistent after being set, due to the Network Manager Service changing its value. The solution was to change the regulatory database to prevent TX power higher then 14 dBm. This held the TX power at 14 dBm.

**Long-term Solution**

This issue is specific to the ESPRESSObin, since the LibreRouter mPCIe interfaces are designed to meet the power requirements of the HPM5G at 19 dBm. In later parts of this document, we will also describe a board modification that will allow us to power the HPM5G properly on the ESPRESSObin.

### Uninitialized MAC Addresses on the HPM5G

Both HPM5G radios were brought up with the same MAC address of `00:02:03:04:05:06`, which prevented two devices from talking to each other.

Additionally, the ESPRESSObin interfaces themselves seemed to be the same as well. This is an unrelated bug in Armbian.

**Work Around**

Setting the MAC address manually allowed the two devices to mesh together.

The ESPRESSObin interface issue was resolved by regenerating a unique machine ID and rebooting:

```
sudo mv /etc/machine-id /etc/machine-id.old
dbus-uuidgen | sudo tee /var/lib/dbus/machine-id
sudo cp /var/lib/dbus/machine-id /etc/machine-id
```

**Long-term Solution**

This issue is specific to the sample units and will not be an issue when the HPM5G is manufactured for production.

## Sending to an Omnidirectional TOP-GS07 USB Radio Through Walls

The first test we did to confirm the device was functioning was to connect an ESPRESSObin + HPM5G node to a Orange Pi Zero + TOP-GS07 node, using 802.11s mesh point. These two devices were about 25 feet apart separated by three drywalls, without line-of-sight, and with desks and file cabinets in between. The ESPRESSObin has the HPM5G transmitting at 15 dBm, its 12 dBi antenna pointed in the general direction towards the omnidirectional antennas on the Orange Pi Zero.

![Office Map](../images/20180530_hpm5g-radio-tests3.png?raw=true)
![Receiving Node](../images/20180530_hpm5g-radio-tests4.jpg?raw=true)

The results of this first test were very impressive. The HPM5G was the transmitter, and the TOP-GS07 was the receiver:

```
Connecting to host 192.168.100.4, port 5201
[  4] local 192.168.100.1 port 52190 connected to 192.168.100.4 port 5201
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  4]   0.00-1.00   sec  5.02 MBytes  42.1 Mbits/sec    0    465 KBytes
[  4]   1.00-2.00   sec  5.25 MBytes  44.0 Mbits/sec    0    465 KBytes
[  4]   2.00-3.00   sec  8.85 MBytes  74.3 Mbits/sec    0    465 KBytes
[  4]   3.00-4.00   sec  8.79 MBytes  73.8 Mbits/sec    0    465 KBytes
[  4]   4.00-5.00   sec  6.63 MBytes  55.6 Mbits/sec    0    465 KBytes
[  4]   5.00-6.00   sec  8.20 MBytes  68.8 Mbits/sec    1    465 KBytes
[  4]   6.00-7.00   sec  9.44 MBytes  79.2 Mbits/sec    0    465 KBytes
[  4]   7.00-8.00   sec  10.5 MBytes  88.4 Mbits/sec    0    465 KBytes
[  4]   8.00-9.00   sec  10.0 MBytes  83.9 Mbits/sec    0    465 KBytes
[  4]   9.00-10.00  sec  10.0 MBytes  84.2 Mbits/sec    0    465 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  4]   0.00-10.00  sec  82.8 MBytes  69.4 Mbits/sec    1             sender
[  4]   0.00-10.00  sec  81.9 MBytes  68.7 Mbits/sec                  receiver

iperf Done.
```

These are the highest speeds we have observed from the TOP-GS07. The HPM5G is transmitting a very strong signal through all these physical barriers, and with low jitter:

```
Accepted connection from 192.168.100.2, port 43694
[  5] local 192.168.100.4 port 5201 connected to 192.168.100.2 port 47881
[ ID] Interval           Transfer     Bandwidth       Jitter    Lost/Total Datagrams
[  5]   0.00-1.00   sec   120 KBytes   983 Kbits/sec  0.299 ms  0/15 (0%)
[  5]   1.00-2.00   sec   128 KBytes  1.05 Mbits/sec  0.545 ms  0/16 (0%)
[  5]   2.00-3.00   sec   128 KBytes  1.05 Mbits/sec  0.560 ms  0/16 (0%)
[  5]   3.00-4.00   sec   128 KBytes  1.05 Mbits/sec  0.494 ms  0/16 (0%)
[  5]   4.00-5.00   sec   128 KBytes  1.05 Mbits/sec  0.432 ms  0/16 (0%)
[  5]   5.00-6.00   sec   128 KBytes  1.05 Mbits/sec  0.466 ms  0/16 (0%)
[  5]   6.00-7.00   sec   128 KBytes  1.05 Mbits/sec  0.388 ms  0/16 (0%)
[  5]   7.00-8.00   sec   128 KBytes  1.05 Mbits/sec  2.240 ms  0/16 (0%)
[  5]   8.00-9.00   sec   128 KBytes  1.05 Mbits/sec  1.051 ms  0/16 (0%)
[  5]   9.00-10.00  sec   128 KBytes  1.05 Mbits/sec  0.800 ms  0/16 (0%)
[  5]  10.00-10.04  sec  8.00 KBytes  1.79 Mbits/sec  0.802 ms  0/1 (0%)
```

HPM5G reported RX:

```
signal:         -75 [-75, -77] dBm
signal avg:     -72 [-73, -75] dBm
```

TOP-GS07 reported RX:

```
signal:         -50 dBm
signal avg:     -50 dBm
```

## Testing a Pair of HPM5Gs

Placing two ESPRESSObins with HPM5Gs about 20 cm from each other, and lowering the TX power to 5 dBm, I was able to confirm speeds of over 160 Mbps.

## Testing the LibreRouter Antennas

We married an Orange Pi Zero with a TOP-GS07 USB radio to the 12 dBi LibreRouter antenna for a long distance test. In the past, we have not had good range or speeds with this board, but since the board supported 5 Ghz and was 2x2 MIMO it was a good test.

We mounted the device with antenna outside to test, with the ESPRESSObin + HPM5G at the other end of the connection to compare RX quality:

![Outdoor mount](../images/20180530_hpm5g-radio-tests5.jpg?raw=true)
![Orange Pi Zero antenna assembly](../images/20180530_hpm5g-radio-tests6.jpg?raw=true)

The devices were about 220 m apart:

![Antenna test map](../images/20180530_hpm5g-radio-tests7.jpg?raw=true)

The positioning of the antennas were not optimal, however with this quick test the TOP-GS07 was able to see the HPM5G with -70 dBm, while the HPM5G could see the TOP-GS07 with -54 dBm. Speed was only 10 Mbps, however the link was very stable.

The antenna case can even be modified to fit the Orange Pi Zero inside.

![Orange Pi Zero antenna assembly 2](../images/20180530_hpm5g-radio-tests8.jpg?raw=true)
![Orange Pi Zero antenna assembly 3](../images/20180530_hpm5g-radio-tests9.jpg?raw=true)

## Bridge Test

On a Tuesday afternoon we took the pair of ESPRESSObins to the bridges where we ran our [Cantenna Field Test](./20170311_cantenna-field-test.md) last year. The distance is approximately 300 m.

![Bridge test map](../images/20180530_hpm5g-radio-tests10.jpg?raw=true)

### Portable Power

We powered one ESPRESSObin with a portable AC power source. The other we attempted to use a 3-cell lithium polymer 1600 mAh battery wired into the DC barrel connector.

When fully charged the battery put out 12.5 V (12.6 V being the absolute max) and the ESPRESSObin seemed to work well with this setup. The test drained the power of the battery to about 50% of its capacity.

### Test Setup and Results

We split up into two teams and connected a laptop to the USB port of the ESPRESSObin to record results, pointing the antenna in the general direction of the other team. One device had TX power of 15 dBm (but it occasionally reboots due to drawing too much power over the mPCIe) and iperf3 recorded speeds close to 100 Mbps. The other device with TX power of 14 dBm never reboote, but it does not reach the same speeds when it's the one transmitting.

This is what one side looks like: 

![Bridge test self](../images/20180530_hpm5g-radio-tests11.jpg?raw=true)

And looking out to the peer:

![Bridge test peer](../images/20180530_hpm5g-radio-tests12.jpg?raw=true)

## Powering the HPM5G Externally

Dragino confirmed that what we were experiencing sounded like it could be a power issue, where the radio was draining more power from the ESPRESSObin than it could provide. After speaking with the engineer they provided a hardware modification to power the radio module externally, instead of via the mPCIe interface. It involves disabling of the 3.3 V to 5 V up-conversion circuit so that we could apply our own 5 V external power, by removing a surface mount resistor and grounding one of the pads.

![Power instructions](../images/20180530_hpm5g-radio-tests13.png?raw=true)
![Power modifications](../images/20180530_hpm5g-radio-tests14.jpg?raw=true)

The modified HPM5Gs look like:

![Modified HPM5G](../images/20180530_hpm5g-radio-tests15.jpg?raw=true)

Using the 5 V power from the ESPRESSObin's hard drive connecter, we were able to successfully power the boards externally using a modified cable:

![Modified cable](../images/20180530_hpm5g-radio-tests16.jpg?raw=true)
![Externally powered setup](../images/20180530_hpm5g-radio-tests17.jpg?raw=true)

After Removing the regulatory lockout in Linux, we were able to bring the radio module up to 26 dBm and run an endurance test for 10 minutes using iperf3 in both directions without the ESPRESSObin rebooting. This shows the earlier issue was indeed power related and the modification successfully fixed it. The power levels observed here is inline with what was reported by LibreRouter in [their earlier tests](https://librerouter.org/article/first-outdoor-radio-and-antenna-test/), which took the HPM5G to 27 dBm TX power.
