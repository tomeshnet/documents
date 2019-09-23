# Babled MR16 Network at Our Networks 2019

# Location

Our networks 2019 was hosted at TMAC.  TMAC has a "art friendly" park outside its front door. This park contains several light poles of recycled wood, painted different colours. These poles also have power outlets that are accessible by permit from the city.


![Physical Map of Network](../images/20190922_outside-view-from-venu.jpg?raw=true)
View from venue.  Red stars indicate placement of antennas.

# Deployment

The deployment contained 4 MR16 nodes in the park, one quipped with an LibreRouter antenna.  Inside the venue at approximately 30 meters there was an MR16 also equipped with a LibreRouter antenna.  This MR16 was connected via a network cable to a EspressoBin acting as a NAT router to the venue's intenet.  Additionally an additional MR16 with a wireguard VPN used the venue's internet to connect back to the exit node and the rest of the experimental babled network.

![Physical Map of Network](../images/20190922-outside-view-googe-earth-venu.jpg?raw=true)
View from venue.  Red stars indicate placement of antennas.


## Physical Map

![Physical Map of Network](../images/20190922_physical-map.jpg?raw=true)

## Logical Map

![Logical Map of Network](../images/20190922-logical-map.png?raw=true)

## Trace Routes

```
ssh root@10.148.10.1
root@NODE148-10:~# traceroute -n 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 38 byte packets
 1  10.188.16.1  1.042 ms  2.160 ms  1.882 ms
 2  192.168.11.11  2.068 ms  1.938 ms  1.783 ms
 3  192.168.0.1  2.511 ms  2.251 ms  6.740 ms
 4  66.207.200.161  23.861 ms  3.521 ms  24.940 ms
 5  72.15.51.246  6.121 ms  3.302 ms  3.181 ms
 6  72.15.49.83  3.885 ms  5.192 ms  3.773 ms
 7  206.108.34.208  9.976 ms  4.003 ms  3.716 ms
 8  1.1.1.1  3.106 ms  3.932 ms  3.463 ms

ssh root@10.159.26.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 38 byte packets
 1  10.10.2.14  20.924 ms  21.341 ms  20.948 ms
 2  11.2.20.1  21.013 ms  27.427 ms  21.420 ms
 3  204.68.252.114  21.709 ms  21.380 ms  21.851 ms
 4  154.54.80.5  21.911 ms  154.54.45.229  21.989 ms  22.004 ms
 5  154.54.40.50  23.130 ms  23.527 ms  154.54.40.30  23.965 ms
 6  38.104.44.10  46.300 ms  78.926 ms  36.243 ms
 7  1.1.1.1  23.611 ms  25.093 ms  22.576 ms
root@NODE159-26:~# 

ssh root@10.182.4.1
root@NODE182-4:~# traceroute -n 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 38 byte packets
 1  10.188.16.1  1.660 ms  0.873 ms  1.104 ms
 2  192.168.11.11  1.723 ms  2.187 ms  1.489 ms
 3  192.168.0.1  2.962 ms  2.199 ms  2.284 ms
 4  66.207.200.161  2.832 ms  8.417 ms  2.944 ms
 5  72.15.51.246  3.660 ms  3.112 ms  2.943 ms
 6  72.15.49.83  4.271 ms  4.001 ms  4.386 ms
 7  206.108.34.208  3.676 ms  3.749 ms  14.498 ms
 8  1.1.1.1  2.535 ms  2.571 ms  2.802 ms
root@NODE182-4:~# 

ssh root@10.188.16.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 38 byte packets
 1  192.168.11.11  0.706 ms  0.874 ms  0.499 ms
 2  192.168.0.1  4.650 ms  3.814 ms  1.395 ms
 3  66.207.200.161  1.790 ms  1.500 ms  1.612 ms
 4  72.15.51.246  7.823 ms  2.612 ms  2.070 ms
 5  72.15.49.83  4.071 ms  2.487 ms  2.609 ms
 6  206.108.34.208  2.517 ms  2.748 ms  4.937 ms
 7  1.1.1.1  2.055 ms  1.737 ms  1.711 ms
root@NODE188-16:~# 

ssh root@10.53.78.1
root@NODE53-78:~# traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 38 byte packets
 1  10.188.16.1  1.005 ms  1.917 ms  0.939 ms
 2  192.168.11.11  1.799 ms  1.445 ms  1.250 ms
 3  192.168.0.1  2.299 ms  2.179 ms  2.048 ms
 4  66.207.200.161  2.601 ms  3.075 ms  3.157 ms
 5  72.15.51.246  3.792 ms  3.982 ms  2.991 ms
 6  72.15.49.83  3.122 ms  3.209 ms  3.278 ms
 7  206.108.34.208  17.086 ms  4.187 ms  4.066 ms
 8  1.1.1.1  2.258 ms  2.600 ms  2.802 ms
root@NODE53-78:~# 
```

![Logical Map of Network Traceroute](../images/20190922_physical-map-traceroute.jpg?raw=true)
Colour lines indicating traceroute results.

# Deployment analysis

## Routing and Links

It seemed the babeld took the least hop count to reach an announced internet gateway.  Looking closer at the directional link, it seems the signal cost may have been to high to try to add another hop into the mix.

The strength of the directional link was the great.  It reported about -75 dBi. Reviewing the data of the two directional node's RX, it appears that at times the antennas must have been pointed better as the signal strength increased to about -69 dBm.

This information was retrieved from the Prometheus database using this query.

```
mesh_node_signal{sourcemac="00:18:0a:35:bc:32",target="00:18:0a:35:b6:06"}
mesh_node_signal{target="00:18:0a:35:bc:32",sourcemac="00:18:0a:35:b6:06"}
```

Resulting view between 2019-09-21 and 2019-09-22:
![RX Signal Strength of antennas](../images/20190922-directional-signal-rx.jpg?raw=true)

## Directional Antenna Mounting

![LibreRouter antenna](../images/20180530_hpm5g-radio-tests2.jpg?raw=true)

Pointing the antennas was a challenge because of several factors. 

- Pole mounted antennas
  - Poles where rectangular making mounting at angles impossible
  - Power was lower down, making height restrictive to length of power cable  

- Pole mounted directional antenna outside  
  - We were not allowed to use the poles at the very front of the venue.
  - We had to mount it on the 2nd pole out.
  - There was no way to adjust the pole mounted antenna left and right
  - The off limit pole was in a line of sight of the venue.

- The Venue's directional antenna inside
  - Mounted by propping it on a ledge in front of the glass
  - No way to mount it
  - It was off to the side as the power cable was not long enough
  - No way to securely mount it
  
Thought: If the directional antenna where pointed more precisely it would be interesting to see how the hops would have changed.  If more hops over better links would be favored over less hops.

# Usage

The venue's network was causing problems with resolving DNS as the DHCP would report 3 DNS servers, but only 1 would work.  This caused some people to use the tomesh.net network instead.

At its peak the network saw about 19 users.

![Network usage](../images/20190922_access-point-users.jpg?raw=true)
