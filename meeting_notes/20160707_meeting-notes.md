---
title: Meeting Notes - July 7, 2016
location: uditvira's
attendees: 6
date: 2016-07-07
startTime: 19:00
endTime: 21:00
---

# Agenda

1. Maker Festival Coordinating
2. Maker Festival talking points (Use cases)
3. Roadmap scheduling and scoping

# Notes

## Maker Festival

### Attendance

- Udit: Sat & Sun
- Ben: Sat & Sun
- Garry: Sat after 2pm
- Claudio: Sat & Sun morning
- Ethan: Sun
- William: Sun morning
- Dawn: Sat & Sun morning

### Maker Festival Materials

- Mesh Workshop Map with markers so people can contribute to the map
- Mounted game board
- Raspberry pi (Reference nodes)
- Cases for the Raspberry Pi (from Creatron for better presentation at the table)
- At least 1 laptop for output from the game board

### Use cases

- World Wide Web Backhaul: Partner with service providers and business partners to provide backhaul
- The concept of a _Big Public Intranet_ as a way of talking about Mesh
- Use case: _Firechat-like p2p messaging application_
  - End-to-end encryption built in via CJDNS versus plain text
  - Application of commercial hardware and open source software to scale the network
  - Solar powered Raspberry Pi's/nodes (self-sustaining infrastructure)
- Use case: _Distributed file hosting_
  - Centralized servers are difficult to scale (Reduce costs for data centres with a distributed FS)
  - Localized file content
  - Optimized for efficiency, but not for anonymity on a mesh
- Discussion point: _Net Nuetrality_
  - Obfuscate packets by default. Equal weighted data on the network
  - No favouritism to types of network traffic and tiered services
- Discussion point: _Encrypted by default_
  - Use of Ethereum and end-to-end encryption
  - Processing power between nodes will determine the performance of the network (encrypted)
  - Mesh should operate on Pi3s and above based on [prototype benchmarks](https://github.com/tomeshnet/prototype-cjdns-pi2/blob/master/docs/phase-1-connect.md#network-benchmark-1)
- Use case: _Non-Internet projects across large geographic distance that require connectivity_
  - [LoRaWAN](https://en.wikipedia.org/wiki/LPWAN) applications like sensor networks
- Use case: _Preloaded content on nodes_
  - Deploying a Wikipedia like service on a mesh
  - Distributed infrastructure to host content (get around expensive infrastructure to host data)
  - [Freenet](https://freenetproject.org/), [IPFS](https://ipfs.io/), [Swarm](http://www.oneswarm.org), as examples

## Roadmap Update

-  **Aim for first week of August (after HOPE and Maker Festival) to regroup and plan out next 6 months**
  - Funding outreach: Agree on a where to channel efforts for funding (e.g. grants, crowdfunding, partners)
  - Collect use cases, and testimonials
  - Create a reference node (software/hardware) to be adapted for other communities and cases
  - Experiment with 900mhz city block coverage. Referring to NYC Mesh's deployments
  - Creation of a web UI, like [RaspAP](https://github.com/billz/raspap-webgui) for TOMesh's nodes
  - Reference: [Enigma box](https://en.enigmabox.net/)
    - Comes with with Internet service and VPN
    - $520 USD
  - Reference: Invizbox (Kickstarter project) [Link](https://www.kickstarter.com/projects/683682172/invizbox-go/description)
  - Kensington deployment as per the workshop map
  - **October**: CJDNS (Untitled at the moment) app based on the VoIP concept from `@benhylau`
    - Android Store working release for October