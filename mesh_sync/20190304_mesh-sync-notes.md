---
title: Mesh Sync Notes - Mar 4, 2019
location: https://appear.in/tomeshnet
date: 2019-03-04
startTime: 10:00
endTime: 12:00
---

📍 https://appear.in/tomeshnet  
📅 Monday, March 4  

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
- benny
- elon
- joseph
- nicopace
- yurko
- tim
- hank (part of meeting)
- garry (part of meeting)

## Agenda

| Start time   | 20-min timeslot                    | Facilitator |
|:-------------|:-----------------------------------|:------------|
|`10:00 am EST`| Intros                             | benhylau    |
|              | General updates                    | yurko       |
|              | Mesh Workshop working group update | benhylau    |
|`11:00 am EST`| Decentralized Web Camp 2019        | benhylau    |
|              | Nico's new role at APC             | nicopace    |
|              | Network drawing activity           | benhylau    |

### Session 1: Intros

### Session 2: General updates

### Session 3: Mesh Workshop working group update
#### Objectives
- Hank released [v0.12: The Remark-able Overhaul!](https://github.com/tomeshnet/p2p-internet-workshop/releases/tag/v0.12)
- Had our first [People's Open x Toronto Mesh workshop meeting](https://hackmd.io/NYlGNIx1TSe4igu3xUWJfQ)
- Roadmap for workshop with modular content based on material from People's Open and Toronto Mesh
#### Links
- http://buildyourowninter.net
- https://tomeshnet.github.io/p2p-internet-workshop/

### Session 4: Decentralized Web Camp 2019
#### Objectives
- Area map and preliminary ideas
- Meshnet equipment for prototyping
#### Links
- https://github.com/dweb-camp-2019/organizing/

### Session 5: Nico's new role at APC
#### Objectives
- Introduce project Nico recently got involved in

### Session 6: Network drawing activity
#### Objectives
- Share results from recent drawing activity at [Toronto Mesh Meet and Greet](https://tomesh.net/2019-02-21/meet-and-greet/)
#### Links
- https://github.com/tomeshnet/documents/tree/master/images/20190221_meetup-drawings/

## Meeting notes

### Intros

- yurko: developing Prototype + everything around tomesh
- joseph (aka. turco32): up for testing things and been helping with supporting new people get set up in chat
- tim: learning the tech, want to help with docs
- nico: part of Altermundi, recently joined APC, planning [Indigineous Connectivity Summit](https://www.internetsociety.org/events/indigenous-connectivity-summit/)
- benny: People's Open, worked with them about a year (firmware debug + exit nodes + workshop + IA antenna coordination)
- benhylau: Toronto Mesh + Our Networks

### General updates

- [Prototype v0.4](https://github.com/tomeshnet/prototype-cjdns-pi/releases/tag/v0.4) released!
    - Lots of features such as Node Profile, Welcome Page, Yggdrasil integrations, etc.
    - Ad hoc on Raspberry Pis tested on 3B/3B+ and Zeros
- LibreRouter
    - Nico can find funding for open source developer for ac drivers
- [Our Networks 2019](https://ournetworks.ca) theme released!

### Mesh Workshop working group update

- Hank [released new theming](https://github.com/tomeshnet/p2p-internet-workshop/releases/tag/v0.12) for the [Mesh Workshop](https://tomeshnet.github.io/p2p-internet-workshop/)! It looks super nice. Now the websites and slides and worksheets are all consistent
- He also manually redrew all the diagrams -> svg
- We ditched gitbook for remark. Now we are generating pdf of slides for all course modules
- Everything is written in markdown (remark presentations, markdown-pdf handouts, jekyll website)
- Want to collaborate with People's Open on a website filled with modular mesh-related workshop activities
- tomesh's workshop is mostly based on Raspberry Pis, but thinking about adding stuff about OpenWRT routers (LibreRouter?)
- nico: Adding modules for LibreRouter sounds excellent! Should be:
    - Practical and need oriented
    - Translatable like [Altermundi docs](http://docs.altermundi.net) (LibreRouter has a translation system)
- yurko: excited :)
- benny: workshop facilitation budget
- benhylau: to share our earlier proposal about workshop facilitations (paying local facilitators)
- nico: responsible for the meshnet component in [techiocomunitario](https://techiocomunitario.net)
    - 3 weeks ago, brought several groups together to learn from each other and it went realy well

### Decentralized Web Camp 2019

- nico and ben went last year -- conference at the mint
- nico: I don't feel like the conversation there has been around decentralized internet infrastructure. Seems like the conversations were mostly around blockchain
- benhylau: Wendy and others mentioned some feedback they received:
    - Too many keynote / sales pitches
    - Not enough use of decentralized services for planning the conference
    - Cost to attend / venue was super expensive
- benhylau: Participation at DWeb 2018:
    - nico did many sessions
    - tomesh did a mesh workshop and a tech demo to livestream with IPFS on Raspberry Pis and LibreRouters
- benhylau: going to create Call for Proposals soon
- This year the venue is a mushroom farm, not a mint, but cost isn't much cheaper because people will live there with meals covered
    - Talking about making entry tier-priced (for people who are supported by organizations or rich on cryptocurrencies they can still pay, but sponsorship should cover cost for people who cannot pay $400)
    - People who help build should get free admission
- nico: How inclusive will this space be? I guess it will be U.S. based, but what about communities in your area?
    - Get in touch with local indigeneous communities
    - Non-coders track
    - Capacity building for non-technical people
    - P2P _not_ D2D (developer 2 developer) or B2B (user in the centre)
    - I think thats the big hurdle for distributed type systems - How do you get the geek-free people to embrace it?
- benny: what is the stated mission?
    - benhylau: TBD this week
- nico: two approaches:
    - Start with a technology, then find a need
    - Start with a need, then work to solve that need
- nico: do it in Mexico next year :) -- this is where offline-living actually makes sense
- benhylau will keep people updated on progress, also [Planning Repo](https://github.com/dweb-camp-2019/organizing/)

### Nico's new role at APC

- Part of [APC](https://www.apc.org) now, responsible for supporting the growth of the community network movement
- [Community Network Project](https://www.apc.org/en/project/local-access-networks-can-unconnected-connect-themselves) with Altermundi and Rhizomatica
- Specific timeframe project
- Building the community network movement
- Include "human technologies": how do we coordinate? Manual and software
- Facilitate conversations around having more gender awareness
- APC Labs
    - Fund and support members to develop and support "long-tail territory" of product development (the 20% polish and support that make things useful as products)
    - Internet Archive and Altermundi are both APC members, so they can both participate in these funds
- InfraCon in BCN around Internet Freedom Festival
- Project has been ongoing for 3 months, mostly been onboarding
- Community peers will be announced
- Project regions: Latin America, Asia Pacific, Africa
- This is an opportunity to listen to communities with needs
- benny: Is there a way to listen without being there in person?
    - Maybe a stack-overflow like thing for capacity building?
    - Video documentation?
- nico: "Hacker In Residence" Project
    - Hackers to live in rural communities
    - Use skills to serve the rural community
    - Prepare yourself to be a servant to someone else
    - Nico will be the guinea pig
    - benhylau: exciting!

### Network drawing activity

- The current prompt is _"Draw what your ideal network looks like"_
- hank: maybe workshop group can start at that as an activity module?
- Sample prompts:
    - benhylau: _"How do we want to build and access digital things"_
    - nico: _"Draw our lives now, then draw our lives with internet"_
- benhylau: we lack spaces for this bidirectional knowledge exchange
    - Community has knowledge of needs where designers have a knowledge gap
    - Designers have skills to build tools which communities lack
- benhylau wants to make space for these exchanges to occur
    - Physical space: challenging (e.g. DWeb at IA vs. at Mexico, either will be a challenge for one of two groups)
    - Sync digital space: ideal but communities aren't online (e.g. Riot/Matrix, WhatsApp, too many platforms)
    - Async digital space: some avenues exist but still limiting (e.g. SSB but hard to share out, nico's video docs)
- benhylau: I find these [Experiences from the ground](https://www.youtube.com/user/nicopace/videos) video docs from Nico helpful:
    - [Yaviche Wireless Community Network NuestraNet](https://www.youtube.com/watch?v=X9womPVhwWg)
    - [Online TV Station in Tlahuitoltepec, Oaxaca, Mexico](https://www.youtube.com/watch?v=Xh4x2PXf9Jw)
- benhylau feels making space for these conversations, and recognizing that the learning is bidirectional, is a shared goal of APC, Internet Archive, Our Networks...
- nico:
    - >There is obviously a lot of smart and creative people in tech, but they suffer from an Achilles Heel trio of weaknesses: self-perceived idealism as excuse, overconfidence in their capabilities outside their own areas of expertise, and lack of attentiveness to details and harms.
      > --[@zeynep](https://twitter.com/zeynep/status/1018459991127314432)
    - Many people agree with this at this meeting
- benhylau: Lots of shared goals among our projects, how to update each other?
    - [APC monthly letter](https://www.apc.org/en/community-networks-and-local-access-monthly-newsletter) from Nico
    - Riot (everyone here is on Riot)
    - Workshop working group will have weekly/biweekly meetings, anyone may join
    - Continue syncing up at biweekly Mesh Syncs (same time for next one and make new schedule after March)

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
