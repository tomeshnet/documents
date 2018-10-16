---
title: Mesh Picnic Notes - September 29, 2018
location: Free Geek Toronto, 180 Sudbury St.
attendees: >10
date: 2018-09-29
startTime: 13:00
endTime: 16:00
---

# Summary

Toronto Mesh partnered with [Free Geek Toronto](https://www.freegeektoronto.org/) for a "Technology Picnic", an opportunity for both organizations to showcase their work.

# Attendees

- dasanchez
- ryan-fgt
- darkdrgn2k
- makeworld
- garrying
- dcwalk
- HeavyMetal
- ansuz
- joeyxl
- Hank

# Activities

## IPFS File Sharing

**Lead**: makeworld

We demonstrated how IPFS can be used to send files from one node to another using a simple web page:

- One node is set up as the "sender" and the other one as the "receiver".
- A user connects to the "sender" node access point and uploads an image.
- A user connects to the "receiver" node access point to view the most recently uploaded image.

### Requirements

- 2x mesh nodes, mesh dongles, and power supplies.
- Power bar for nodes and laptops.
- Power cord extension to hold demo outside.
- Optional: Two laptops (smartphones are OK too).

Visit makeworld's [repo](https://github.com/makeworld-the-better-one/ipfs-demo) for further details.

## Long-Distance Wireless Mesh Link

**Lead**: darkdrgn2k

We showcased a solution for linking an internet exit node with a mesh network over a long distance wireless connection. See below for reference:

![Long range wireless link diagram](/images/20180929_mesh-picnic-wireless-link.png)

- A mesh node is configured as an Internet exit node.
- A LiteBeamAC antenna is mounted on a tripod inside, next to a window and facing outside.
- A second mesh node is attached to the LiteBeamAC.
- A second LiteBeamAC is setup on a tripod/pole outside, with the antenna pointed at the inside one.
- A third mesh node is attached to the outside LiteBeamAC and set up as an Access Point.
- Users can connect to this Access Point for Internet access.
- More mesh nodes can be set up in the vicinity of the outside LiteBeamAC node in order to extend the network.

### Requirements

- 2x mesh nodes (plus an Internet exit node)
- 2x LiteBeamAC
- Optional: Access Point
- AC Power Supplies
- Mounting hardware

## Secure Scuttlebutt Ad-hoc Pub

Several of us managed to send messages to each other through [Patchwork](https://github.com/ssbc/patchwork), [patchfoo](https://github.com/ssbc/patchfoo), and [Manyverse](https://www.manyver.se/) using the available mesh nodes.
