---
title: LibreRouter Bridge Test
location: Toronto
attendees: 6
date: 2018-05-20?
---

# Overview 

We received 6 HPM5G mPCIe 5 GHz single band radio and 6 12dBi antennas from the LibreRouter project to test their effectiveness.  We plugged the mPCIe radios into an EspressoBin running our prototype stack.  The board was identified and the `ath9k` driver installed automatically on boot brining the board up without any issues.  

![HPM5G](../images/20180530_tomesh-HPM5G.jpg?raw=true)

## Power Consumption issues

During the initial setup and testing we noticed that the Espresso Bin would restart at what seemed to be random times. We tried different combination of Radio boards and Espresso Bin boards but the issue was persistent. We tried to reach out to the Espresso Bin community without any luck; however the Armbian community mentioned that this seemed like an issue insufficient power. Identifying this as a potential power issue we tried using larger amperage power supplies (1.5 and 2 amps) however this did not seem to solve a problem.

## Work Around

After identifying a potential power problem we tried to limit the amount of power the Radio would need by reducing the TX power of the radio.  We found that keeping it around 14dBm would cause the Espresso Bin to operate and not reboot.  Our initial testing was then done using a 14dBm TX Power

We did run into an issue where the TX power would not be persistent after being set.  Our initial solution was to change the regulatory database to prevent TX power higher then 14dBm however later we found that the Network Manager Service was resetting the power back to a higher value.

## Initial Desk Test

The first test we did to confirm the device was functioning was to connect to have the Espresso Bin with the 5 GHz Radio connect to a Raspberry Pi with a Toplinkst-rt5572 USB radio.  This device was sitting on a desk in an office 3 offices down from the EspressoBin approximately 25 feet distance.  This was NOT line of sight, with drywall, desks and filing cabinets in the way.  The Espresso bin was set to 15dBm and the antenna pointed in a general direction. 

![Office Map](../images/20180530_tomesh-librerouter-test1-map.png?raw=true)
![Office Map](../images/20180530_tomesh-orangepi-zero.jpg?raw=true)

The results of this first test were very impressive. The Espresso Bin was the transmitter the Toplinkst was the receiver in this test. 

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

And low jitter
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

HPM5G Reported RX
```
    signal:         -75 [-75, -77] dBm
    signal avg:     -72 [-73, -75] dBm
```
Toplinkst Reported RX
```
    signal:         -50 dBm
    signal avg:     -50 dBm
```

## Mac address conflicts

We had issues getting the two Espresso Bins to talk to each other. After troubleshooting we found that each HPM5G had the same mac address set (seems to be uninitialized at 00:02:03:04:05:06).  Setting the mac address manually allowed the two devices to mesh together.

Additionally the Espresso bin interfaces themselves seemed to be the same as well. This is an unrelated bug in Armbian that we resolved by regenerating a unique machine 
ID and Rebooting
```
    sudo mv /etc/machine-id /etc/machine-id.old
    dbus-uuidgen | sudo tee /var/lib/dbus/machine-id
    sudo cp /var/lib/dbus/machine-id /etc/machine-id
```

## Initial Espresso to Espresso Test

Placed the two Espresso bins about 20 cm from each other, and lowered the TX Power to 5dBm. I was able to confirm speeds of over 160Mbps.

## Antenna Test - Orange Pi and Toplinkst-rt5572

We Married a Orange Pi Zero with a Toplinkst-rt5572 USB adapter to the 12dBi antenna for a long distance test.  In the past we have not had good success with this board, but since the board supported 5Ghz and was 2x2 MIMO it was a good test.

We mounted the Antenna outside to test. We used the HPM5G as the other end of the connection to compare RX quality.

![Outside Mount](../images/20180530_tomesh-orange-pi-test.jpg?raw=true)
![OPI Mount](../images/20180530_tomesh-orange-pi-test2.jpg?raw=true)

The test was about 220 Meters away
![OPI Test Map](../images/20180530_tomesh-orange-pi-test-map.jpg?raw=true)

![OPI Mount](../images/20180530_tomesh-orange-pi-test5.jpg?raw=true)

The positioning of the antennas was not optimal however with this quick test the Toplinkst was able to see the HPM5G at -70dBm while the HPM5G could see the Toplinkst at -54dBm.  Speed was only 10Mbps however the link was very stable.

With a fairly good test I reworked the antennas cast to fit the orange pi directly into the case.

![Outside Mount](../images/20180530_tomesh-orange-pi-test3.jpg?raw=true)
![OPI Mount](../images/20180530_tomesh-orange-pi-test4.jpg?raw=true)

Next step will to be to try to add the radio module inside as well

## Bridge Test

On Tuesday Afternoon we took the pair of Espresso Bins to the bridges where we ran our previous Cantenna Test 2 winters ago. The distance is approximately 300 meters.

![Map](../images/20180530_tomesh-bridgetest-map.jpg?raw=true)
### Power

We powered one Espresso Bin with an stock portable AC power source. The other we attempted to use a 3cell Lithium Polymer 1600mAh battery wired into the DC barrel connector.

When fully charged the battery put out 12.5 volts (12.6 being the absolute max) and the Espresso Bin seemed to work well with this setup. The test drained the power of the battery to about 12.15 which was about 50% of its capacity.

### The test
We split up into two teams. We connected a laptop to the USB port of the Espresso Bin to record results, pointed the antenna in the general direction of the other team.

![Near Side](../images/20180530_tomesh-bridgetest1.jpg?raw=true)

![Far Side](../images/20180530_tomesh-bridgetest2.jpg?raw=true)

## Hardware Mod

Reaching out to the LibreRouter team, they confirmed that what we were experiencing sounded like it could be a power issue, where the Radio was draining more power from the Espresso Bin then the Espresso Bin could provide.  After speaking with the engineer they provided a hardware mode for the boards.

The solution was to disable the 3.3v to 5v up conversion circuit so that we could apply our own 5v external power. This meant removing a surface mount resister and ground the resulting pin.
![Instructions](../images/20180530_tomesh-HPM5G-hw-mod-instructions.png?raw=true)

Ben took on the task to modify the board
![Workstation](../images/20180530_tomesh-HPM5G-hw-mod.jpg?raw=true)

The modded board looks like this

![Modded Board](../images/20180530_tomesh-HPM5G-hw-mod2.jpg?raw=true)

![Espresso Bin Mod](../images/20180530_tomesh-espressobinmod-connected.jpg?raw=true)

Using the power of the Espresso Bin’s hard drive connecter (5v rails) we were able to successfully power the boards externally using a modified cable.

![Cable](../images/20180530_tomesh-espressobinmod-cable.jpg?raw=true)

After Removing the regulatory lockout in Linux, we were able to bring the Radio module up to 26dBm and run an endurance test for 600 seconds (10 minutes) using iperf3 in both directions successfully without the EspressoBin rebooting proving that the issue was in fact power related and the mod successfully fixed it.