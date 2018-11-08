---
title: Mesh Sync Notes - Nov 5, 2018
location: https://appear.in/tomeshnet
date: 2018-11-05
startTime: 10:00
endTime: 12:00
---

📍 https://appear.in/tomeshnet  
📅 Monday, November 5  

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
- hank
- yurko
- stigo
- guifipedro

## Agenda

| Start time   | 20-min timeslot | Facilitator |
|:-------------|:----------------|:------------|
|`10:00 am EST`| Course 1        | benhylau    |
|              | Course 2        | benhylau    |
|              | Course 3        |             |
|`11:00 am EST`| General 1       |             |
|              | General 2       |             |
|              | General 3       |             |

### Course 1: Workshop Collaborations
#### Objectives
- Introduce existing collaboration opportunities
- Discuss Toronto Mesh capacity
- Discuss Toronto Mesh asks from collaborators
- Plan next steps moving forward
#### Links
- https://github.com/tomeshnet/p2p-internet-workshop/issues/68

### Course 2: Hardware and Take from IPFS grant
#### Objectives
- Finalize hardware orders
- Decide how to keep inventory
- Agree on Take process for IPFS grant
#### Links
- https://github.com/tomeshnet/p2p-internet-workshop/issues/56
- https://github.com/tomeshnet/p2p-internet-workshop/pull/72

## Meeting notes

### Out of band
*Agenda got hijacked for more than an hour :)*

- stigo: Working on
  - Web portal (stigo did a demo)
  - Blog post of Oslo week
- stigo: https://github.com/stigtsp/cjdns-hello
  - Uses the perl [cjdns_tools](https://github.com/hamishcoleman/cjdns_tool) so it can run on mesh-orange
  - benhylau: This may be useful to integrate into web portal:
    - https://github.com/tomeshnet/prototype-cjdns-pi/blob/master/scripts/ipfs/nodeinfo-ipfs
    - https://github.com/hyperboria/docs/blob/master/cjdns/nodeinfo-json.md
  - yurko: https://github.com/darkdrgn2k/prototype-cjdns-pi/compare/master...darkdrgn2k:Web?expand=1
- benhylau: Integrate Yggdrasil to prototype/mesh-orange, would be nice if web portal can support that too
- stigo: Want to set up more mesh nodes at Hackeriet venue
  - WiFi range, stability issues with SDs, are concerning for rpi, can there be other options?
  - yurko: Rock64? But you definitely need a directional for range
  - yurko: No upgrade path
  - stigo: Try mesh-orange
  - benhylau: Since need is immediate, use commercial router, plug Pi into it
  - hank, yurko: LibreRouter
  - Resiliency and opportunity to experiment with p2p-web are the objectives
- guifipedro: eXO.cat of the guifi community
  - RetroShare (compared to SSB, with metadata protection)
  - Running WiFi network with static IPs, flash router with final configurations, compatible with idea of flashing routers + plug in Raspberry / Orange Pi
  - Freifunk random address assignment: https://github.com/freifunk-bielefeld/firmware/tree/master/package/simple-radvd
    - Random addresses vs. Guifi planned network approach
    - https://gitlab.com/guifi-exo/wiki/blob/master/info/research-projects.md#network-descriptor-proof-of-concept
    - guifipedro: BMX6 neighbourhood + rigid BGP Barcelona backbone, there is nothing wrong with that
    - guifipedro: Rigid BGP protocol, it's good that we have something to agree on, and local communities can run whatever local protocol they need
    - Someone posted RouterCity in the chat
    - Are there better ways to bridge two networks without agreeing on BGP? e.g. cjdns and Yggdrasil
    - benhylau: libp2p circuit-relay?
    - guifipedro: Some people _do_ want centrally managed networks
    - guifipedro: Not having an issue with necessitating an autonomous system
    - benhylau: But someone must manage the BGP announcements still in a Guifi type network
    - guifipedro: Fiber links in Guifi are very static
    - So what exactly are the issues with BGP? Park for next time!
- benhylau: We will park this routing protocol discussion and perhaps invite Yggdrasil developers, Moritz from Freifunk, and others to the next call to continue this discussion

### Course 1: Workshop Collaborations

- benhylau explained current collabs on https://github.com/tomeshnet/p2p-internet-workshop/issues/68
- benhylau: For Guifi there was some interest in IPFS, see http://proto.school
- guifipedro: Larger group in Guifi looking to run workshops, guifipedro will hang out here and find fit
- hank: Workshop too simple vs. too complex during TPL facilitation, did we revisit?
- guifipedro: Make a real role-playing scenario of an activity (e.g. activist, police) helps explain abstract concepts like metadata privacy
- benhylau: This is very good :) more role-play explanations integrated!
- Difficulty levels for each module? But we have limited capacity as Toronto Mesh to support workshop
- hank: Whether students would be able to reuse this information? (think TPL group)
- hank: Pursuing collab and work on syllabus
- benhylau: Try to engage digital justice community in Toronto
- yurko: Want to run this again in full, but again, capacity
- benhylau: Anyone interested in helping with coordinating this with partners, please comment on issue:
  - https://github.com/tomeshnet/p2p-internet-workshop/issues/68
- guifipedro: Version of the course run on VM, solves a lot of problems
- benhylau: Talk to stigo! hamish is going to build mesh-orange for x86 and release iso, so stigo can put this into some cloud/hypervisor:
  - https://github.com/tomeshnet/mesh-orange/issues/57
  - Practically I think 2019 Q2 for this to be ready

### Course 2: Hardware and Take from IPFS grant

- Did not have time to discuss this item
