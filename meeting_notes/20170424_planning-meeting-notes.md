---
title: Meeting Notes - April 24, 2017
location: Semaphore Studio 307, Claude T. Bissell
attendees: 10
date: 2017-04-24
startTime: 18:30
endTime: 21:30
---

# Agenda

1. Intros (0:10)
2. Recap (0:30)
  - TOmesh so far...
  - Previous Planning Meeting
  - Working Areas and Recent News
2. Current Decisions (0:50)
  - Discussion around Kensington Market Deployment
  - Funding
  - Governance
**BREAK**
3. Future Directions (1:20 min)
  - Partnerships
  - Deployment 
  - Roadmap

# Notes

## Intros

- We will use voting in this meeting to reach consensus and help keep to time:
    - _Thumbs up_: go ahead, care about the issue and happy with direction
    - _Closed fist_: "no-block"
    - _Thumbs down_: needs more discussion, feel strongly enough to block
- Covered agenda for meeting

- Dante: learning about mesh networks, experience with hardware on mechanical side. Interested in solar-powered reference node, collected data and ready for analysis (connections to San Diego)
- Udit: interested in hardware stuff, background in electrical side. Secondary projects on low-power wireless networks (IoT sensor networks)
- Garry: background research in networks and infrastructure. website lead and generalist
- Pedro: interest in deployment and thinking about a low-cost wireless ESIP model and mesh network
- Josh: interested in hardware and monitoring technology (as well as agricultural monitoring projects)
- Benhylau: working on reference hardware node, infrastructure. Shifting to Orange Pi software image and hardware that would improve communicating between nodes, address current ambitions (e.g. social and technical)
- Adam: working with Kensington Market
- Hank: growing interest in graphic design, hardware, installing, free time in the summer!
- dcwalk: cerntral organizing and interested in moving away from that

## Recap

### TOmesh so far...

- Started ~16 months ago, thinking about models for organizing, how to think about governance and strategy over the next 6 months
- Outreach: events around networking literacy workshops, connecting to other groups, building reference hardware and software
- Looking about how to build capacity long term, previous projects including Wireless Nomad (then bought by Cogeco)
- Look to a parallel project as a model for how we could work? (Pittsburgh "MetaMesh" process of identifying community, hosting install nights)
- Opportunities around a mesh implementation for internet-sharing

### Previous Planning Session

- Recall [our notes from November 12](https://github.com/tomeshnet/documents/blob/master/meeting_notes/20161112_planning-meeting-notes.md)

### Working Areas and Recent News

1. **Tools** (benhylau)

  - Infrastructure maintenance (website, kanban, chat server, permissions and security)
  - Anticipating physical nodes and device level monitoring
  - Needs: served over the internet, looking to have stuff accessible over CJDNS, looking to automate in a more "DevOps" way, software that can be accessible over the website
  - Projects: Onboarding with a chat bot
  - Interest in learning: Pedro

1. **Central Org** (dcwalk)

  - Event planning and adding to the website, work with other leads to streamline if needed
  - Coordinating with selecting a time, adding event posts, coordinating space
  - Making sure meeting minutes get on the website
  - Interest:

1. **Virtual Mesh** (benhylau)

  - Bi-weekly meeting to (virtual) and in-person but looking for another person to take over leading it
  - Interest:

4. **Deployment** (udit)

  - Made connecting with TPL, through two channels, in order to partner with deploying nodes
  - Next step: demo of nodes in order to move that forward
  - Could good be a good fit with someone who already has access or a location in mind
  - Interest: Ben interested in helping, Pedro in semi-leading

5. **Website** (garry)

  - Relatively self-sustaining this past section
  - Upcoming projects: Integrate node map into website (Pedro has been testing)
    - thinking about how a user would add stuff to the map
    -	could node let you know if it is live
  - Interest: Dawn, Garry

6. **Funding/Grants** (anastasia)

  - Took a step back on funding after a round of submitting grants and conversations about capacity. This does constrain potential deployments
  - Process for putting in grants was developed

7. **Onboarding, Welcome, Intros** (josh_o)

  - Outreach at events, also welcoming new people to the chat, answering the hello email

## Current Decisions

### Discussion around Kensington Market Deployment

- [Kensington BIA](http://www.kensingtonmarketbia.com/)
  - 10k startup, 3-4k operating cost
	- looking for a turnkey solution?
  - willingness from businesses to participate
  - provide consistent service
  - want to know more information about data about foot traffic
- Looking for February 2018 rollout to cover wifi access points in 2018
- Adam submitting final report Wed, presenting at a board meeting next month

**BREAK**

## Future Directions

### Funding

Are there immediate plans to pursue funding over the summer?
- No one is currently pursuing securing funding sources
- Not anticipating any shared tomesh expenses over the summer, revisit depending on deployment

### Governance

_Are people interested in any of the working groups?_

Tools: Benhylau, Dante, Pedro, Udit... lower scale?  
Central: Dante (**L**), Dawn  
~~Virtual Mesh:~~ Ben, Udit (rename "Hack Sessions" and run headless?)
Deployment: Udit, Pedro (**L**), Hank  
Website: Dawn (**L**), Garry  
~~Funding:~~  
Outreach: Pedro (**L**), Udit, Ben, Dante  
node.tech: Ben, Udit (**L**), (_Ceit.e_)  
_node.local_  

### Deployment/Partnerships

_What partnerships do we want to pursue?_
- Toronto Public Library
- Kensington

_Where do we want to deploy?_
- We are not at the stage where our tech is reliable for large-scale deployment
- Realistically not gonna have mainstream adoption SOON

_What are the immediate next steps?_
- Build mapping and monitoring tools (reproducible across local networks), track the virtually-meshed nodes
- Answer key hardware and implementation questions (e.g., best antenna sub 2km)
- Goal: first physical link (2 balconies)
- Outreach revisit with TPL: work sessions, learning about networking
- Adding more application use-cases for raspberry pi prototype (e.g., [streama](https://github.com/dularion/streama), [kodi](https://kodi.tv/), and [patchwork](https://github.com/ssbc/patchwork))

### Roadmap

_What are the key milestones?_

1. apply for makerfest
1. restart conversations with TPL
1. bi-weekly node.tech meetups over the summer
1. public hardware workshops
1. map up on our website
1. test network (2 nodes with physical link >100m)

_Who needs to be added to what services?_ (Tools working group)
  - hello@tomesh.net
  - github admins
  - ssh keys servers
  - moderators in chat rooms
  - Digital Ocean accounts
  - tomesh.net domain

#### Key Dates

April 30: Outreach Makerfestival Deadline **Udit**
mid-May: Integrate Map with **Website**
end-May: Outreach develop 2 pitches for tomesh to TPL
end-May: Virtualmesh documentation improvement
mid-Jul: Makerfestival
end-Dec: Mesh Orange a platform we can run off of (better, iterable)

How we will work:
- bi-weekly Hardware (node.tech) meeting in-person
- monthly virtual mesh
- monthly install party & social
