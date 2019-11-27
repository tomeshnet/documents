---
title: Mesh Sync Notes - Feb 18, 2019
location: https://appear.in/tomeshnet
date: 2019-02-18
startTime: 10:00
endTime: 12:00
---

📍 https://appear.in/tomeshnet  
📅 Monday, February 18  

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
- Ben

👥 Please add your name to this list if attending:
- Hank
- Ben
- Dante
- Tim
- Yurko
- Felix
- joeyxl
- CJD
- Pam

## Agenda

| Start time   | 20-min timeslot | Facilitator |
|:-------------|:----------------|:------------|
|`10:00 am EST`| Course 1        |             |
|              | Course 2        |             |
|              | Course 3        |             |
|`11:00 am EST`| General 1       | benhylau    |
|              | General 2       | dasanchez   |
|              | General 3       |             |

### General 1: Decentralized Web Camp 2019
#### Objectives
- Brief on ideas being discussed in the organizing of DWeb Camp 2019 in July
- Discuss opportunities for event meshnet with local off-Internet applications
#### Links
- https://www.decentralizedweb.net

### General 2: Toronto Mesh outreach things
#### Objectives
- Feb: Toronto Mesh monthly [Meet and Greet](https://tomesh.net/2019-02-21/meet-and-greet/)
    - Drawing activity at our next one on Feb 21
    - General intro / onboard "package" previously discussed
- March: participate at [CodeAcross](https://www.eventbrite.ca/e/codeacrossto-2019-tickets-53330824933)
- April: opportunity to [speak at CivicTechTO](https://github.com/tomeshnet/documents/issues/112)
- May: opportunity to [organize activity at Pegah's UofT event](https://github.com/tomeshnet/documents/issues/111)

## Meeting notes

### Prototype updates

- In process of releasing next version (final stages of testing)
    - Adds yggdrasil (can give IP addresses to LAN devices not running yggdrasil, encryption done by Raspberry Pi)
    - Cleaned up install scripts and added **Profiles** (finally!)
    - Version bumps + other optimizations
    - Welcome screen:
        - cjdns + yggdrasil logical map
        - live bandwidth numbers
        - list of services running on the node
    - ben: we can use this welcome screen for intro to new people
    - yurko: help with testing https://github.com/tomeshnet/prototype-cjdns-pi/pull/291
    - yurko: next release will focus on debianizing modules
    - ben: so we need https://github.com/tomeshnet/mesh-services/issues/8

### Decentralized Web Camp 2019

- https://www.decentralizedweb.net by Internet Archive
- 2019 conf: Camp @ Mushroom Farm - maybe
  - Broken Internet as a "feature"
- 2018 had SSB, IPFS, and others, but not a lot of meshnet representation (backpack for hope was there)
- Offer some sort of "local services" stack- IPFS repository, SSB pub, etc.
- benhylau is looking into coordinating Toronto Mesh representation this year
- LibreRouter is nearing production- hopefully after Chinese New Year
- List of people to reach out to:
    - [Aether](https://getaether.net) (Burak)
    - [SSB](https://www.scuttlebutt.nz)
    - [DAT](https://beakerbrowser.com)
    - [IPFS](https://ipfs.io)
    - [Yggdrasil](https://yggdrasil-network.github.io) (Arceliar + Neil)
    - [CJDNS](https://github.com/cjdelisle/cjdns) (Caleb)
    - [LibreRouter](https://librerouter.org) (Nico)
    - [Manyverse](https://www.manyver.se) (Andre)
    - [Cabal](https://cabal-club.github.io) (noffle)
    - [Disaster Radio](https://disaster.radio) (People's Open)
    - [Matrix](https://matrix.org)
- Cheap routers for access points:
    - Meraki + OpenWRT
    - Aruba Networks AP (Used a lot at other conferences)
- See [our meeting notes](https://github.com/dweb-camp-2019/organizing/pull/1/files)

### Toronto Mesh outreach things

- Feb: Toronto Mesh monthly [Meet and Greet](https://tomesh.net/2019-02-21/meet-and-greet/)
    - Drawing activity at our next one on Feb 21
        - Prompt for drawing activity?
            - **How do you think connectivity works** vs **how do you want it to work**?
        - The former is already understood by tomesh people, but it would help identify pain points to improve upon.
        - Focus can be on technical and non-technical aspects.
        - What do we do with the output? Digitize and publish:
            - On SSB
            - Make a story/gallery with all the sketches
            - Save media for OurNetworks exhibit
        - hank: 11' x 17' scanner
        - dante: bring papers
        - tim: bring roll of paper
        - ben: bring markers
        - Outline:
            - _Draw how internet works today, then... draw how do you want it instead?_
            - _Draw your cyber world, then... draw how to improve your pain points?_
            - Present afterwards
            - Broad (draw whatever you want) vs. focused (draw your ideal node user interface and how you interact with it)
            - ben: we should be able to string together a story from the drawings and put a SSB post
            - hank: _maybe_ volunteering to "compose some stuff" with the drawing _at some point in time_
    - General intro / onboard "package" previously discussed
        - What is tomesh and what does it do? A 5-10 minute intro would be good to introduce newcomers
        - felix: Freifunk (since 2003):
            - People come and want to set up router (usually)
            - Depends on level of engagement
        - pam: People's Open:
            - First Tuesday of the month -- pizza, hangout, TCP/IP zines
            - Sunday afternoon office hours (2-3 ppl organizers) -- Google Form for people who want to set up a node
            - Mapping list of projects
        - [tomesh project page](https://tomesh.net/projects/)
            - pam is referring to a geographic map (project is a physical site, e.g. IA)
        - pam:
            - laptops for all (fixing up donated hardware)
            - learning to set up a node (Sunday afternoon), a new person shows up, someone from People's Open will walk me thru setting up of a node
            - _Steward_ assigned to a person to help them navigate "the mesh"
                - ben: I think this is a great model that perhaps Toronto Mesh can use
                - ben: Our project page shows "current" projects, but it's hard to navigate how pieces fit together
                - Model of pairing up with someone (face-to-face or otherwise) would be great for onboarding newcomers: talk about our projects/help them set up a node/install Patchwork or Beaker Browser
        - benhylau and ryan_fgt are working on a grant proposal for turning FreeGeek into a hackerspace on Sundays
        - Current [tomesh workshops](https://tomeshnet.github.io/p2p-internet-workshop/)
            - Less network focused than it is p2p focused
        - felix: Internet is the number one service on our mesh network :)
        - pam: p2p web, people are like _what_??
        - felix: go to bars, actually get internet (2 guys built a network that became 200+ nodes)
        - Decouple "elaborate p2p stack" with "connectivity stack"
        - yurko: backhaul over existing Internet connections (piggy off home Internet and VPN over somewhere)
            - felix: this is how we do it
            - ben: let's exit on felix's german infra
        - ben: maybe using People's Open's stack is well-aligned with our near-term:
            - dweb (meshnet + raspberry pis plugged in)
            - educational curriculum co-development
            - openwrt transition to librerouter hardware
        - cjd: ipredator? goes thru sweden
- March: participate at [CodeAcross](https://www.eventbrite.ca/e/codeacrossto-2019-tickets-53330824933)
    - ben is going, dante may go
- April: opportunity to [speak at CivicTechTO](https://github.com/tomeshnet/documents/issues/112)
    - dante can go and speak, he will ping patcon to arrange dates
- May: opportunity to [organize activity at Pegah's UofT event](https://github.com/tomeshnet/documents/issues/111)
    - Event centered around privacy and censorship as it pertains to artistic work
    - Toronto Mesh-run Workshop?
        - perhaps our "drawing activity"
    - Email Pegah on activities we can run- dante will email Pegah re: dates
 - Tim: [SWIFT network](http://swiftnetwork.ca/) could be a partner even if it's just for running a workshop
    - ben: I wonder if it shares similarity with [XOC](https://www.xarxaoberta.cat)
    - tim to reach out to find out more
 - Tim: check out the [Development License](https://www.ic.gc.ca/eic/site/smt-gst.nsf/eng/sf11373.html) option for radio spectrum work

## Communications load balancing

| Organization | Toronto Mesh contact | Subject | Status |
|:-------------|:---------------------|:--------|:-------|
| Toronto Public Library | @benhylau @dcwalk @darkdrgn2k | Mesh Workshop | Completed pilot, interested in next iteration |
| Florida Polytechnic | @Shrinks99 @darkdrgn2k @benhylau | Mesh Workshop | [Agreement to collaborate](https://hackmd.io/-9P_SzjKSROHUj8zEE_qqw?view), shipped some parts to Florida and got the group set up to facilitate module-1 |
| Guifi.net | @benhylau | Mesh Workshop | Completed module-1 facilitation + helped translate worksheet to _es_, discuss future opportunities |
| Palo Alto Library | @benhylau | Mesh Workshop | Introduction via Wendy (Internet Archive), had a [first call](https://github.com/tomeshnet/documents/blob/master/meeting_notes/20181107_workshop-series-intro-for-city-of-palo-alto-library.md) |
| NYU Abu Dhabi | @benhylau | Mesh Workshop | Discussed with Michael about using syllabus at the university during Radical Networks 2018 |
| Design Exchange | @Shrinks99| Workshop collab | Had first call and relayed asks at February 4 Mesh Sync |
| Internet Archive | @benhylau | Decentralized Web Camp 2019 | Early planning started with notes on [dweb-camp-2019/organizing](https://github.com/dweb-camp-2019/organizing) |
| CivicTechTO | @dasanchez | April Hacknight | Getting dates from CTTO |
| Pegah @ UofT | @dasanchez | May event workshop | Will contact Pegah re:dates |
| SWIFT | Tim | not specific yet | Will ping and see what they are doing |
