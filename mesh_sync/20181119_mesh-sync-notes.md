---
title: Mesh Sync Notes - Nov 19, 2018
location: https://appear.in/tomeshnet
date: 2018-11-19
startTime: 10:00
endTime: 12:00
---

📍 https://appear.in/tomeshnet  
📅 Monday, November 19   

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
- elon
- ryan
- yurko
- stigo
- melissa
- (a couple guests)

## Agenda

| Start time   | 20-min timeslot | Facilitator |
|:-------------|:----------------|:------------|
|`10:00 am EST`| Course 1        | benhylau    |
|              | Course 2        |             |
|              | Course 3        |             |
|`11:00 am EST`| General 1       | benhylau    |
|              | General 2       | benhylau    |
|              | General 3       |             |

### Course 1: Hardware and Take from IPFS grant
#### Objectives
- Finalize hardware orders
- Decide how to keep inventory
- Agree on Take process for IPFS grant
#### Links
- https://github.com/tomeshnet/p2p-internet-workshop/issues/56
- https://github.com/tomeshnet/p2p-internet-workshop/pull/72

### General 1: Tools sharing
#### Objectives
- How to use Loomio to asynchronously and remotely establish consensus on a topic
- Discuss recent issues with our matrix.tomesh.net
#### Links
- https://www.loomio.org
- https://loomio.cryptography.dog

### General 2: IPFS Live Streaming @ IPFS All Hands
#### Objectives
- Who wants to participate?
- Plan online + demo on Nov 26
#### Links
- https://github.com/tomeshnet/ipfs-live-streaming

## Meeting notes

### Out of band

- ryan: Winter Haven community, setting up smart park:
    - Two people from community may be able to lead this technically
    - Entrepreneurial focus + social benefit
    - Regional fiber hub in Winter Haven (200 ft from park), like New Jersey having the hub at the country
    - Arts in public space, engage local library system, engage public
- ryan: Student group progress:
    - Received adapters from Toplinkst, waiting on Pis and USB headers to arrive
    - Students able to reproduce the Module 1 set up
    - Students able to get cjdns message -> robots
    - benhylau: Larger cjdns community interested in research in meshing in changing topologies
    - Short-term, planning an activity with city, test run at Winter Haven park
    - "Junkyard hacks" as a concept
- ryan: Some people to introduce project related to MANET:
    - `TODO` benhylau to send ryan:
        - Freifunk refugee Internet
        - Standing Rock examples of providing semi-transient/semi-permenant WiFi to communities
    - benhylau: Manyver.se for mobile + Patchwork for desktop (both based on Secure Scuttlebutt)
    - benhylau recommends designing for limited network accessibility to start
    - cjdns is bad at churny MANET topologies
    - `TODO` yurko to send notes on using Raspberry Pi WiFi to mesh in ad-hoc mode
- ryan: Pi network interface / cjdns telemetry:
    - See: https://github.com/benhylau/mesh-workshop/
    - See: https://tomeshnet.github.io/p2p-internet-workshop/articles/module-5/pdf-assets/module-5.pdf
    - Use cjdns `peerStats`, showing: MAC, cjdns switch port, connection status, in/out, packet loss (peerStats available on prototype but not on mesh-orange)
- stigo: Updates on recent works:
    - peerStats stuff -> web UI
    - `TODO` benhylau stigo: to get perl [hamishcoleman/cjdns_tool](https://github.com/hamishcoleman/cjdns_tool) into debian package (so both mesh-orange and prototype can share it)
    - stigo: unit testing framework that runs on the device

### Course 1: Hardware and Take from IPFS grant

- benhylau went over status of hardware orders
    - LoRa boards: vendor shipped the wrong thing, in refund process
    - SD cards and Toplinkst radios shipped
    - Waiting on Raspberry Pis and USB headers
- benhylau to start Take process for IPFS: similar to SSBC grant but in CAD, once PR is merged benhylau will write a cheque
    - Consensed on process

### General 1: Tools sharing

- Identified that it's likely we have a memory leak (python2.7 synapse process > 1.5g in `top`) in this version of Synapse + Python (we upgraded both, issues occur after Python version upgrade)
- Probably swapping a lot based on the stats
- Long-running query, unsure if related:

    ```
    SELECT pid, now() - pg_stat_activity.query_start AS duration, query, state FROM pg_stat_activity WHERE (now() - pg_stat_activity.query_start) > interval '5 minutes';

      pid  |    duration     |                                                                                 query                                                                                  | state
    -------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------
     19091 | 00:44:16.281082 | DELETE FROM stream_ordering_to_exterm WHERE room_id IN ( SELECT room_id FROM stream_ordering_to_exterm WHERE stream_ordering > 2180040 ) AND stream_ordering < 2180040 | active
    (1 row)
    ```

- Live debugging inconclusive
- Take offline to continue investigation

### General 2: IPFS Live Streaming @ IPFS All Hands

#### Logistics
- Monday 26th, not sure what time yet
- Using Zoom for video call
- `TODO` benhylau to prep slides based on yurko's Our Networks slides
- `TODO` benhylau to email Portia to confirm details
- `TODO` benhylau, yurko, and elon to prep devices and test setup next weekend
    - Prep a fallback setup already running that elon can stream to

#### Goals
- benhylau would like people to feel comfortable using it
- Want audience to have an opportunity to understand its inner workings (detail the flow of information in this system)
- Highlight differences vs. HTTP (advantages over deploying on a traditional webserver on S3)

#### Plan
- Start spinning up a cluster and talk thru steps (yurko)
- Spend 10 minutes to thru slides (yurko):
    - Start with motivations for this project: _Toronto Mesh for Our Networks 2018_
    - Introduce components
    - Follow data flow
    - Talk about IO and scability
    - Talk about Our Networks setup
- Show that cluster successfully brought up with terraform (yurko)
- Show URL for audience to navigate to live player (yurko)
- Copy OpenVPN keys to OBS device in background (elon)
- Share OBS screen then starts streaming a demo video to new live instance (elon)
- Hey! You can do this on a Raspberry Pi + some router, and here is the repo (yurko)
- Pain points we discovered (yurko):
    - [IPNS is broke on Internet DHT](https://github.com/tomeshnet/ipfs-live-streaming/issues/3)
    - IPNS needs at least two nodes to work at all
    - IPNS requires time sync between the two nodes, NTP not guaranteed on offline systems
    - Speed performance and bandwidth use concerns
    - Why is ipfs.io cluster not as performant as infura.io?

#### Misc notes
- IPFS Chrome/Firefox plugin
- ipfs-js? It doesn't do DHT
- Drop ffmpeg and switch to rtmp plugin in nginx
- HLS events (and its compat issues across browsers)

---

These have nothing to do with anything but they're here:
- http://node2.e-mesh.net/quake3/
- https://ipfs.io/ipfs/QmZrNZjkYM2keC1NHk5VKxD1e4Fqpr6QTBcX52cijBjmRG/
