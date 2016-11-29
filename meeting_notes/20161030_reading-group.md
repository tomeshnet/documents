---
title: Toronto Meshnet: Inaugural Reading Group - October 2016
location: HackLab.TO, 1266 Queen St
attendees: 8
date: 2016-10-30
startTime: 13:00
endTime: 15:00
---

[tomesh.net/2016-10-30/reading-group-oct/](https://tomesh.net/2016-10-30/reading-group-oct/)

Present
---------

- ansuz
- dcwalk
- vector
- jon
- Anastasia
- weltgeist
- 2 guests

Topics
-------

### Discussing Reading Group Format

- the need that a meshnet addresses is more obvious in a rural setting where users don't otherwise have access to networking
- what does Toronto need that a meshnet can provide?
  - ???
- Jon hopes that this could be a "blue-sky" reading group where we could cover things that we wouldn't in a workshop setting
- short stories could maybe have a place in future readings
- "Book reports" so that not everyone has to read every article might also be worthwhile
  - The person who chose each paper could be responsible for this
  - time always slips away from us, and *reading is hard*
    - low commitment in that even if you haven't read everything, you're still welcome
- Maybe we need a cap on the number of pages per reading?
- Weltgeist and Ethan are interested in reading *The Master
    Switch:*
    <https://www.amazon.fr/Master-Switch-Rise-Information-Empires/dp/0307390993>
    - but this is a full book and people won't be able to commit to that
- Anastasia is still stuck on the subway
  - lol Toronto

### Reading

#### Ethan: The City that was Saved by the Internet

- <https://motherboard.vice.com/read/chattanooga-gigabit-fiber-network>
- previously a heavily-polluted industrial town
- Chattanooga wanted to lay fiber, Comcast was opposed because
*the government shouldn't compete with private industry*
- In Toronto this is comparable to the situation with Bell/Rogers vs Wind, Teksavvy, etc.
- They laid Fiber, and it's been great for the local economy
- There is now a startup community drawn to the city
- We're not laying down fiber, so we don't have that problem
- Where can we deploy our infrastructure so that it serves the greatest number of users?
- How do we deal with *entrenched interests*?
- Maybe Toronto isn't the right location for this because of the high rent
- Toronto has poor IPv6 adoption, so the capacity to host content from otherwise restricted networks is a potential benefit
- Especially with the offer of VPN setups where clients can be assigned a public IP address for home computers (as opposed to in a datacenter)
- we may need to gather evidence and test deployments in a
less restrictive environment before moving forward

#### Anastasia: Deploying Rural Mesh Networks

- <http://eprints.gla.ac.uk/34544/1/34544.pdf>
- deploying meshnets in rural areas
- How many users are in the town?
- Wikipedia: Wray, Lancs, UK 2001 pop: 521
- technical problems may be easy to fix
- user regulation is difficult
- p2p applications can easily use all available bandwidth
- users are overly optimistic
- user education is the most viable option for improving quality for everyone
- "most people in a community need to communicate *with each
other*"
- LocustWorld nodes were owned by users
  - the tech spec: <http://ftp2.za.freebsd.org/pub/mesh/pc/locustworld/ftp.mirror.ac.uk/sites/live.locustworld.com/lwmbtechspec.pdf>
- What do we have in terms of performance monitoring?
- not much, finn (of Seattle meshnet) does a lot of monitoring
- Charlie (of NYCMesh) does a lot of monitoring as well
- What are our expectations about how we would use the stack?
- "We're waiting for a *killer app"*"
  - **Our current stack is a little bit shaky**
- QoS is fairly well explored, the issue of user expectations is harder to understand
- Apparently lots of community mesh networks have had to deal with software getting abandoned
- it's nice having Hyperboria supporting this tech, but users on the ground may still be responsible for updating
- we should look to automate as much as possible

#### dcwalk: Macroscopically Sustainable Networking

- <http://www1.icsi.berkeley.edu/~barath/papers/quine-limits16.pdf>
- What should the goal of a network be?
- Qual.net is mesh networking software that ships with a
captive portal that distributes its own source code
- <https://github.com/WachterJud/qaul.net>
- A network should be able to produce new components using
local resources
- What are the dependencies of a network?
- we rely on integrated circuits (mostly from China)
- supply chains that ship parts to users
- Electricity
  - maybe we should be using social?
- <https://cradlepoint.com/blog/jeremy-cramer/woktenna-my-homemade-antenna-3g%E2%80%89%E2%80%93%E2%80%89cradlepoint-action-photo-contest>
- We want a mesh network that is self-propogating
- inb4 the world ends cause of us
- two questions:
  1. maybe we need to think about alternative internets...
    - pigeons <https://tools.ietf.org/html/rfc1149>
    - sneakernets/community dead-drops
      - not relying on continuous connectivity
  2. question two???
- Connecting nodes at all times might be a security risk?
- instead of hosting your services in California, keep it in Toronto
- <https://en.wikipedia.org/wiki/The_100-Mile_Diet>
- dynDNS attacks took down large services on the internet
  because everyone centralized around them
  - apparently this was entirely avoidable using dns caching, but clients need to configure that, so that's an issue
- Toronto Hydro Infosec Guy met at Defcon (Tim)
- Hydro is building their own mesh network in case other infrastructure goes down
  - they can't be reliant on various telCos to provide their infrastructure
- Maybe by saying "we're going to build a mesh network" we've put the technology first, and not the use case
- "the world is full of problems"

#### Micheal: Internet of Things

-     <https://www.schneier.com/blog/archives/2016/02/the_internet_of_1.html>
- "World-Sized-Web" as an autonomous robot
- Sensors, Actuators, Logic
- Google has access to absurd amounts of data
- Cars are connected
- People can't turn off their lights in their smart home when the internet goes down
  - lol
- <http://www.zdnet.com/article/the-night-alexa-lost-her-mind/>
- What kind of world are we building?
- it's hard to predict the direction of the future
- we didn't really predict social media or the effect it would have
    - citation needed
- corporations and governments retain as much information as they can
- "make surveillance expensive"
- re: destroying data
- you can only destroy your own data
- <https://transitiontech.ca/cjdns/cjd>
  - "I have nothing to Hide" --cjd
  - maybe a worthwhile read re: open data and
    arguments:
    - against ephemerality
    - in favour of sous-veillance
- IoT:
- there will be an increasing need for network capacity as
  more devices connect
- delivering data via trucks
- <http://www.theverge.com/2015/10/7/9471381/amazon-snowball-data-transfer-device>
  - thanks udit!

Next Steps
-----------

- Meeting last Sunday of the month, next one November 27.
  - Anyone is welcome regardless whether they chose a reading
- Pick new readings within the next week, by November 7.
  - Impose a cutoff time for selecting readings so we have more time
    to finish
- Themes we want to look more at:
  - Pedagogical issues re: network literacy is something to take
    advantage of (toronto community network)
  - Mesh case studies (at least one)
    - detroit, red hook
    - <https://gigaom.com/2012/12/18/detroit-is-the-testing-ground-for-a-new-open-source-wireless-network-technology/>
  - Also open to things which are
    - speculative
    - philosophical
  - History of networks?
    - <https://www.amazon.ca/Where-Wizards-Stay-Up-Late/dp/0684832674>
  - Toronto meshnet as related to *digital divide*
    - *pain points*
- Remember: 10am November 12th, planning session
  - action plans
- dcwalk will post more reminders about the reading group soon
