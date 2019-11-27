---
title: Mesh Sync Notes - Mar 18, 2019
location: https://appear.in/tomeshnet
date: 2019-03-18
startTime: 10:00
endTime: 12:00
---

📍 https://appear.in/tomeshnet  
📅 Monday, March 18  

| Timezone | Start time |
|:---------|:-----------|
| PST      | `07:00 am` |
| EST      | `10:00 am` |
| CEST     | `03:00 pm` |
| HKT      | `10:00 pm` |

## What is this?

Biweekly open calls to sync up on topics relating to the global Community Network movement. The hours are selected to make it possible for parties of different timezones to attend.

Anyone may propose a topic on [this open-edit pad](https://hackmd.io/HSOK15u7TnS6Oz1RH0McGg), taking one of five session timeslots by putting yourself as _Facilitator_ and filling the corresponding [_Agenda_](#Agenda) section. You can see previous meeting notes on [tomeshnet/documents/mesh_sync](https://github.com/tomeshnet/documents/tree/master/mesh_sync) to get an idea of what type of topics have been discussed in the past.

Please scope your session within a 20 minute time block. If more time is needed, it is probably best to use the 20 minutes to give an overview, then schedule separate meetings with interested parties. The hope is that these standing hours can be well attended and everyone participating gets a general idea of global initiatives relating to the Community Network movement :satellite:

## Attending

📝 This person moves meeting notes to GitHub and resets the pad:
- benhylau

👥 Please add your name to this list if attending:
- ben (benhylau)
- caleb (cjd)
- yurko
- tim
- pedro (guifipedro)

## Agenda

| Start time   | 20-min timeslot   | Facilitator |
|:-------------|:------------------|:------------|
|`10:00 am EST`| Intros            |             |
|              | cjdns update      | caleb       |
|              | Session 2         |             |
|`11:00 pm EST`| Guifi update      | guifipedro  |
|              | DWeb Camp update  | benhylau    |
|              | Future mesh syncs | benhylau    |

### Session 0: Intros
#### Objectives
- Introduce and connect with each other on the call

### Session 1: cjdns update
#### Objectives
- Talk about recent progress on cjdns
#### Notes
- If supernodes are permissionless, what prevents them from flooding the network with routes and every supernode's memory blows up?
- Proof-of-work on route announcements by supernodes
- Source routing (cjdns) has an issue where someone can trash a link by bouncing a packet around two nodes indefinitely by crafting a route label that way
- TCP gives backpressure information for Yggdrasil
- Supernode resource usage: 1 core of a 3 GHz machine (but the supernode code is a nodejs prototype)
- Supernodes mine _announcements_ (like Aether)
- Block miners mine _blocks_ (gather data generated and make routes)
- Supernodes max out CPU resources
- Supernodes: Announcement miners for ETH, Block miners get a discount on PoW (both collecting announcemets) 
- Supernodes: Gather data about peers, quality of nodes 
- Supernodes communicate with each other operationally, block miners will want same info just to capitalize on for discounted routing.
- Radio metrics -> Supernodes (announce routes) -> Block miners (secure blockchain and through that make bandwidth leases)
- Supernodes buy from bandwidth market and resell that bandwidth to the local network, make money on mark-up in this competitive market
- Some analogies:
    - Block miners are doing make work
    - Supernodes are like ISPs without infrastructure
    - Physical infrastructres are owned by anyone
- >We are separating ISP from their infrastructure and the infrastructure is owned by whoever
    - ben: this shares a lot of similarity with guifi.net ISPs
- caleb:
    - Watch out for pre-mines and ICOs
    - But there are always winners and losers (people who came early)
- Promote to user audience / early adopter, but not cryptocurrency communities
- ben: Forks?
    - caleb: Don't need to defend against that, we should have more credibility
- Thoughts about permissioned blockchain?
    - Not decentralized, based on community trust
    - As sidechain to do escrowed exchange (BTC <-> Mantle)
    - e.g. Liquid
- tim: Dfinity, high transaction rate
- Blockchain may not be able to pay for its own development:
    - Relying on generosity of miners
    - Don't want ICO
    - A Founder's fee (like zcash) better because it pays out overtime, but too centralized
    - Can't democracy vote because we don't have IDs
    - Don't really like any of the above, how to make people be held accountable?
- "most-money-wins" election:
    - Vote for or against a neetwork steward (which is a key that gets to spend the tax) as part of a transaction
    - If more than half the money is voting against the current steward, an election is triggered
    - Network stewards cannot spend more than 3-month old funds (taxes collected have an expiry)
    - Network stewards may finance software development, buying infrastructures, lobby for airwaves, etc.

### Session 3: Guifi update
- Long time without contacting you, I have fresh news: these days guifi is in a crisis
#### Objectives
- Share our recent experiences with guifi. It's also a good moment to do a live Q&A about the project.
#### Notes
- Guifi is in crisis
- 90% of network traffic is managed by for-profit operators (https://es.wikipedia.org/wiki/Sociedad_de_responsabilidad_limitada), lacking biodiversity
- Guifi Foundation made the compensation system for operators to equilibrate between network usage and investment of the network as a strategy to prevent exploitions (or extractive economy)
    - As a consequences, some operators joined efforts doing nearly monopolies on their region of operation
- There are evidences that guifi Foundation have problems implementing the model or operating over it (this is something that all agree). Big operators are exploiting this vulnerability because they want to grow more (and as they are big enough they need less and less help)
- Big operators want to change collaborative framework to be more "like Internet".:
    - Limit the tighly collaboration-cooperation: Personal conflicts between core participants of the network are very present
    - Large operators want to exit with majority of the network (they claim that their networks belongs to them; this is not clear and the situation could end in courts)
    - They talk about operators, quitting participations to volunteer and user roles
- Concern: they are claiming the property of a shared infrastructure that may eventually be sold or participated by a major operator / they could be considering shared infrastructure as endorsement of their loans.
- This is like a hostile change from GPL -> MIT license (not by consensus)
- As operators grow they become different in character, started as volunteers but become more protective of enterprise over time (perhaps because of burdens of loans, etc.)
- caleb: Is there an infrastructure that generates the problem?
    - pedro:
        - With wireless is mostly fine, CAPEX is low, OPEX is high
        - Problem is with optical fiber deployments (CAPEX) that involve lot of investment. The stuff that the ISPs are claiming ownership now. Because OPEX is low, and they want to speculate/regulate it as they want. (I see analogies here similar to water and energy after the infrastructure is already deployed)
- Currently, the big operators intent to continue collaborating, but concern they will eventually defect
- Top4, [operadors.cat](https://operadors.cat), is an example of operators that become monopolies within their region
- Looks like the Guifi agreement prevents operators from becoming rich; that's why they want to change fundamental rules
- Battlemesh in Paris in July :beers: https://framadate.org/12ORCCBq1H4b6fjy
- Now we (associations and cooperatives operators) are in negotiations between operators and guifi foundation
- Next month we have to present our proposal. Operators present a new proposal. Foundation present another one. In June we have to merge the three documents (if possible)
- caleb: It's possible that the current agreement is what keeps them (Operadors) in the first place
- Negotiator should realize that... probably if you guys defect you will all turn around and screw each other
- Change [FONN](https://benhylau.github.io/talks-and-workshops/talks/201810_nuug-hackeriet/#29) or economic model?
    - ben: FONN is like your constitution and that's the bottom line?
- caleb: Is the proposed change to get rid of protection for users of network / small operators?
    - pedro: Right now, "compensations" regulates decisions in zones "one operator one vote". The change want that only operators participate (not users or volunteers) and with a weighted vote based on investment. So yes, it favors big players.
    - Looks like they want to get rid with some of the protections (to become more rich?). A good analogy is the origins of Internet, it started as a project where public administration, militaries and universities did heavy investment but the profit was for private parties. Transition from public to private end up (or it was a big step) when Internet God John Postel dead in 1997 heart operations caused by this privatization process/problems
- Continue conversation on matrix chat
#### Links
- guifi.net
- fundacio.guifi.net
- https://gitlab.com/guifi-exo/wiki/tree/master/info/2019-proposta-canvis-guifi
- https://operadors.cat

### Session 4: DWeb Camp update
#### Objectives
- Update on DWeb Camp 2019 planning so far
#### Notes
- Made new repos and matrix channels
- Feel like building a new Internet? [Please comment on these issues](https://github.com/dweb-camp-2019/meshnet/issues)
#### Links
- https://github.com/dweb-camp-2019/organizing

### Session 5: Future mesh syncs
#### Objectives
- Discuss post-March mesh syncs
    - New time?
    - New facilitator?
#### Notes
- ben is traveling in April and May and cannot facilitate Mesh Syncs
- No new facilitator at the moment for April and May, so we may pause
- tim _may_ take on facilitation
- We need to repoll for new time, and move to jitsi

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
