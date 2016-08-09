---
title: Planning Meeting Notes - August 5, 2016
location: HackLab.TO
attendees: 14
date: 2016-08-05
startTime: 19:00
endTime: 23:30
---

# Agenda

0. Intros (10 mins)
1. TOmesh so far... (20 mins)
2. Non-tech WiFi research group update (15 mins)
*Break (10 mins)*
3. Organization (40 mins)
4. Mesh deployment strategy (30 mins)
5. Funding (15 mins)
6. Roadmap (40 mins)

## Intros (10 mins)

- We will use voting in this meeting to reach consensus and help keep to time:

    - _Thumbs up_: go ahead, care about the issue and happy with direction
    - _Closed fist_: "no-block"
    - _Thumbs down_: needs more discussion, feel strongly enough to block

- Agenda for meeting
- Names, general areas of interest, level of involvement so far

## TOMesh so far...

Project started when the group who share this common interest met at [CivicTechTO](www.meetup.com/Civic-Tech-Toronto/). We discussed and agreed what the issues are that we care about and put that into our Vision Statement.

Talking with other mesh networks. There are large, sustained meshes in Barcelona and Germany, but North America hasn't been able to sustain large-scale community mesh networks.

We believe we can't just focus on building the tech. Must grow the community and distribute the knowledge on how to maintain it. Must scale community with the mesh. Want to develop technical literacy education modules as part of growing the community to maintain their own part of the infrastructure.

### Reference Node Prototype (Raspberry Pi)

Tech platform -> Raspberry Pi. Initial idea to flash routers, but they are becoming increasingly locked down. Interested in a platform that is a lot more flexible. Distributed network running a bunch of distributed applications.

- Focus on security and privacy at the protocol layer
- Not advocating neglecting security at the app layer, but security at IP layer also makes sense
- [cjdns](https://github.com/cjdelisle/cjdns) allows for IP allocation to also be decentralized

#### Setting Up

[Platform based on Raspbian](https://github.com/tomeshnet/prototype-cjdns-pi2):

	- Flash SD card and run a line of code and the Pi will reboot and talk to one another
	- Connect through SSH to node remotely, end-to-end encrypted

#### Existing Examples

Existng cjdns meshes:

	- [Hyperboria](https://fc00.org) (a virtual mesh) has 700+ nodes globally
	- Wireless Slovenia uses cjdns and has 1000+ nodes (some scalability issues but they're doing it)

#### Range Testing

- Only a few test nodes in Ben's apartment
- Tested them in Bahen Center in a straight line
- We need to go to a park and test
- HackLab has roof access with line-of-sight to places
- Doesn't necessarily have to be line-of-sight [(see Fresnel zone)](https://en.wikipedia.org/wiki/Fresnel_zone)
- Possiblity to explore different bands:

	- SDR
	- UHF
	- TV Whitespace
	- 900 MHz (900 MHz for VOIP, use WiFi exclusively for other data)

#### Privacy and Anonymity

No, it's not anonymous, but you can run TOR over cjdns. Anonymity is hugely inefficient. With cjdns you get security but not anonymity. When you start a node you generate a public and private key. The public key is used to derive an IP, creating an identity that doesn’t depend on central authority. When you speak to a node you are doing source routing, nodes are constantly discovering paths. You decide your path to the end node. Use keys to encrypt packet to negotiate a shared secret with the destination node, then encrypt the communication with that shared secret. Throw away the shared secret after that session. This ensures forward secrecy.

### Maker Festival

Satellite "Intro to Networks" Workshop on June 25 & "tomesh.mini" game on July 6 and 7 during Makerfestival Extravaganza. Outreach where we built a game board. Learned what people care about.

One thing we realized early on was that we had a hard time connecting with people about why this is important and what we are trying to do. Brainstormed and came up with a game to showcase what the problems are with centralized systems. In the board game, you connect parts of city and it would bring down parts of your system and you had to reconnect, demonstrating the faults of centralized system. Kids interested. Using a Raspberry Pi instead of a modem was great to get people involved on a lower level than just talking about mesh itself.

### HOPE – NY

Ben and dcwalk connected with other mesh projects at [HOPE XI (Hackers on Planet Earth)](https://xi.hope.net). Spent lots of time with NYC mesh guys. Oakland sudomesh people were there. A lot of people agreeing that we need a distributed ownerless last-mile network and a step to having free access to info where interests are aligned with people who use it and not the telecoms.

On hardware side we want open platforms, but also want them to be cheap.
This is part of building mesh tech in Toronto, but want to be portable to other countries. Frequency bands may differ in other countries. Frequency agnostic system is one goal. Build the right levels of abstractions.

Various initiatives in NYC. Group that's working with BATMAN, but also initiatives to move away from BATMAN because there are issues and there isn't a lot of in-house expertise with deep knowledge of BATMAN. Install process is painful. You have to downgrade AirOS and flash OpenWrt. Hard to self set up. Some people want to switch to cjdns.

We don't want to set up for people, it's unsustainable and against our principles of user ownership. [Getting a node working shouldn't be rocket science.]

Lots of interest from other mesh groups and people involved in mesh projects. In near future lets get everyone in the same place. International event and invite everyone to come to Toronto.

First, have a virtual space for local meshes to communicate. [Vector](https://vector.im) and [Matrix Homeserver](http://matrix.org), an open federated chat app and protocol. Instead of being tied to Slack. We generally like to run things ourselves instead of depending on centralized services.

### Vision Statement

- Current vision statement, which has received lots of feedback about changes:

> The internet is currently not open and inclusive for all people. We are building a community-owned infrastructure that gives us:
- open, lower-cost **access** to the World Wide Web
- a **resilient** and redundant network
- **agency** to make important decisions about privacy
- **autonomy** to access information in a free manner
- an opportunity to develop **technical literacies**

- Decided during [April 18, 2016 planning meeting](https://github.com/tomeshnet/documents/blob/master/meeting_notes/20160418_meeting-notes.md)
- [Minor tweaks and discussion on June 28](https://github.com/tomeshnet/documents/blob/master/meeting_notes/20160621_meeting-notes.md#e-update-from-ottawa)
- [Relevant Pull Request](https://github.com/tomeshnet/tomesh.net/pull/19)

- Last time we talked about this:

	- We all cared about these things but not necessarily in the order presented
	- Presentation of vision impacts how it relates to funding
	- Wording may be confusing for some
	- At the time we didn't have a deployment project

### Code of Conduct

- Previous consensus to adopt a Code of Conduct, work in progress: [WIP Code of Conduct](https://github.com/tomeshnet/documents/pull/23)
- tomesh as an organization has put thought into human dynamics and care about being nice to each other
- Having *enforceable* Code of Conduct is important, but enforcement in a distributed system can be difficult
- Important to establish that "being good to each other" culture, get it entrenched early on, otherwise it's hard to recover
- Also concerned about how people can screw with the system, malicious intent, etc.
- Agreed to establish a working group on CoC

## Non-tech WiFi Research Group Update

Intro about efforts so far. Considering target communities, weighing need for something like this in community, how well it satisfies tomesh's needs for test deployment (we haven't really talked about this with tech group), what local resources available, community connections, symbiotic initiatives, funding. TCH looks good, especially with Nahum's connections in such communities and programs happening there. Researching where we have the best access to go in and actually do something there. Orton Park has most meat on bones in terms of access for us, but also looking into Swansea (High park), Firgrove (Jane/Finch), Kensington Market.

Starting to discuss door-to-door research with residents and other community members to gather data. What do people in these communities lack and desire? Met Toronto Star Data Lab director and in contact with ACORN, who together have experience doing door-to-door surveying and mapping maintenance issues. Could be very useful for us in terms of how to interact with these communities, how to create consistent and useful questionnaires, how to compile and analyze data effectively and efficiently with minimal staff.

We've been talking about developing Maker culture in these communities to increase technical literacy required for sustainable mesh deployment.  Have discussed even creating our own Maker spaces or working with other orgs to do it. Evolving Maker programs to include networking and Raspberry Pi's, mesh concepts, etc. [This is one point where ideas and pre-requisites for tomesh deployment divergefrom main goals.] Gathering local support and recognition of mesh in communities.

[Read Nahum's outreach doc since he is not in attendance]

- tomesh needs to figure out how much of the literacy component we are prepared to do with the limited capacity
- There's an organic aspect out of growing this project, perhaps the community will just happen naturally

### Mesh to Provide Low-cost Internet

- A lot of people are interested in low-cost Internet, but the mesh technology may not be the most straight-forward way to get there:

	- e.g. What throughput can we get out of tunnelling through cjdns?
	- Eventually we may have an [Airbnb for ISP](https://github.com/tomeshnet/mesh-isp)
	- Hard to commit to a timeline (hard to, at this moment, plan a low-cost access project)

- Low cost access is not the sole focus of tomesh, other focuses like security and decentralization
- Shouldn't just start providing low-cost access or change direction to do that
- Should make sure we have the security aspect ready from the get-go
- Removing barriers to access as the on-ramp, make things a little bit more fair so everyone can play. Cost aspect was a piece of that, but so was education

It's not just cost. We've been forcing telecoms to give up some of their infrastructure, coffee shop WiFi, etc., but it hasn't solved the problem because we didn't change the ownership model. We need to change the ownership model. We [who have Internet access] don't go to the library to loan out a Raspberry Pi to go online. Why should we expect anyone to? We should all have the same level of access.
- Use mesh as last-mile, cellphones to exit to the Internet from home ISP plan. So many ways this can go

- We do have a plan for accessing Internet over the mesh, but it is still an early draft:

	- [Plan from a discussion in NY](https://github.com/tomeshnet/mesh-isp)
	- Anyone can be an ISP, selling upstream bandwidth to the Internet downstream to clients
	- Minimal knowledge about clients
	- Bitcoin transaction to sell portion of your upstream bandwidth to others, exactly like buying a VPN with Bitcoins

### In-mesh Use Cases

Number one barrier to adoption is what are people already doing and how do you get them to do it on the mesh. Going to challenged communities, kids go to McDonalds because they don't get kicked out. That forum good for VOIP, cat pics, piracy, whatever. But if it doesn't have wider Internet and access to what people really need, they will not adopt.

There are also others with completely local use cases in mind:

- Local sharing economy:

	- If you want a tool, like a hammer, you will get the closest tool to you. The Internet is local, sharing economy. If we can make [...] we have a network for everyone to be able to find a service or product and should be able to use the mesh to find that
	- But how can you connect people to the community better than Facebook, and how does mesh network itself enable that?
	- Local sharing economy is one of many local services that can be run _in-mesh_, as with any of these services, you can share it over both Internet and mesh

Long-term, it's not about gatewaying to the Internet. It's about pulling the Internet into the mesh network. Just put an antenna on the roof and you are now providing the same service over the local mesh (in addition to the Internet). ISP (Internet gateway) running on mesh is also one of the services.

- Use cases where using mesh can directly help (e.g. industrial automation, community-owned infrastructure to connect up hardware across the city)

We all have houses and community, and sitting in the same room. Let's form a mesh ourselves, starting with a virtual mesh over IP.

- Lets make a map of where we are (but there are privacy concerns)
- Agreed on starting a virtual mesh
- Agreed to in the next non-tech group meeting, figure out what the group's primary goals are, then bring it back to the general tomesh group and see where the efforts fit

## Organization

### Tools and practices

Talk about choices about tools used. Open-source and decentralized. Information structures should not be on other people's computers. Open-source, data ownership, facilitate an interaction that is public and not closed participation. Nobody in charge of managing accounts. Github does that because of forking and pull request features. International groups able to copy and adopt and adapt information according to relevancy to them.

If you develop something, you are [responsible for documenting it](https://github.com/tomeshnet/documents/tree/master/service_setup). Don't have central points of failure. If you have something that needs authenticated access, share access with at least a couple of people so if you disappear it doesn't get lost or become unusable. Don't share password. Make multiple admin accounts.

Meeting notes should be kept for all meetings. Made available to everyone. Current process is to write on a Riseup Pad, then transfer to [this Github repo](https://github.com/tomeshnet/documents/tree/master/meeting_notes).

[Introduced existing tools like Github and Wekan]

- Some feel completely lost with our current set of tools, in terms of usability
- Currently hosted on Digital Ocean since it provides the uptime we need
- Lee offered a server to host tomesh tools, where we can have physical access
- [Kune](https://kune.ourproject.org) as a platform:

	- Similar to Crabgrass, a sharing and collaboration tool with various types of content, tools, features. But many strengths over Crabgrass. Run your own installation on your servers. Extensible using WRT to change whole software or anyone can use Java/Python to easily create apps and bots. (People decide what plugins they want to use individually). Uses single-page dynamic content like Gmail and Twitter rather than static page PHP where browser has to load entirely new page to navigate. All documents and tools are *Waves*. Waves are abandoned Google Wave product that is now open/libre. Wave is a document that can be anything, e.g. a wiki or a calendar or voting poll or video or text document. Kune creates some default profiles and interactions for waves suitable as common and familiar tools and puts them all in one place. Objective is to replace centralized, single purpose services like Gmail, Twitter, Google Docs, IM, Wikipedia, Youtube, etc., with all-in-one dynamic, libre, federated product you control, and do in such a way that anyone can pick up and use intuitively. Also contains chat that is compatible with Gmail Chat and other apps. If you have account on one Kune server you can interact with content and users on any other Kune installation. Basically, it's a beautiful thing... on paper. None of us has explored it yet. I just read all the documentation and FAQs, etc., about it.
 	- Leandro to explore Kune by creating account on Kune.cc and others should too
 	- Comparison to Crabgrass in regard to ease of managing our own installation on local servers

- Build automation:

	- Nothing to CI (continuous integration) build at the moment, since we only have simple install scripts
	- Larger projects like cjdns are already on build automation
	- Chat bots could be a very helpful automation

### Logo

[Didn't spend much time talking about this, someone should just do it]

[Leandro: I didn't mention this because we moved on too quickly and I was taking notes, but branding is a very important thing. It communicates everything about you, even a "feeling" that people take away when exposed.  There are groups that can help develop the identity and image of any initiative according to their needs to very effectively deliver ideas with heavy and memorable impact. The logo, the name, the colours, even vision statements. It does matter. It's not about corporate tactics. It's about human psychology, science, and smart communication.]

### Website

[Showed our existing website and its current features]

Suggestions:
	- Landing pages to get people up to speed about what we're about
	- Need intro to what is mesh, and links for further info
	- Blog page of what's going on (content from collaboration, progress, discussion on wiki, etc.)
	- Show task progress by linking to our publicly readable Wekan (write access requires authorization)

## Mesh Deployment Strategy

- Start with a series of workshops:

	- [Build a Mesh Node](https://wekan.tomesh.net/b/LWS8X7sGFXqDgZ7ag/tomesh-net/J3ztC365p6k9NXPyN)

		- Know what it is we are actually talking about
		- Take home to start this virtual mesh
		- Try to do some in-mesh use case
		- Try gateway to the Internet over cjdns
		- One member has $1300 allocated for mesh development (plan to buy [Raspberry Pi and TL-WN722N](https://github.com/tomeshnet/prototype-cjdns-pi2#set-up) for each attendee)
		- Discussed whether Raspberry Pi is the best platform, mixed opinions, but it's what we know works at the moment
		- Other platforms like Pine64, ODROID, C.H.I.P. were brought up, and perhaps we can hack those too at this workshop
		- Run as skill-share and just show up with a vague idea of what you want to accomplish

	- [Toronto Internet Infrastructure](https://wekan.tomesh.net/b/LWS8X7sGFXqDgZ7ag/tomesh-net/LirG95Mxtdu85J44i)

		- How Toronto is connected
		- ISP industry knowledge (Free-Net, Bell, Rogers)
		- Make a [showoff deck](https://github.com/tomeshnet/tomesh.101#running-presentations) and host it

	- [Build a Bot](https://wekan.tomesh.net/b/LWS8X7sGFXqDgZ7ag/tomesh-net/jC9yoXidcT5tQTHbq)

		- Many people have expressed interest in this
		- Help automate a lot of our tasks, especially documentation

## Roadmap (6 Months from August to January)

### Funding

- There is a pitch document to apply for government funding, it's been posted on Slack
- Canadian sovereignty if we have own infrastructure, instead of relying on external providers
- Ethan knows more about funding opportunities through government, but he isn't in attendance
- Free-Net can apply for funding

### Legal Status of TOmesh Organization

- The organization may need some sort of legal status if we need to accept funding
- NYC mesh is associated with [Internet Society](http://www.internetsociety.org)
- tomesh may be able to operate through Free-Net, etc. so we don't need to deal with legal status and insurance
- Free-Net is a not-for-profit with a mandate to support "alternative networking group of Toronto", Lee as ED for the non-profit is happy to have tomesh apply for funding through Free-Net
- Small community bank account to avoid having to set up a non-profit (some members have set up such accounts and there is almost no maintainence aside from a few dollars of monthly fee, you are essentially running as a community soccer club)
- Agreed we need a working group to sort out our legal status, but no one is interested
- Agreed that we should wait other members' presence to resume this discussion

### Permanent Space

Several people offering space:

	- Hugh runs internet TV station "That Channel", offering space and show time (need someone who can represent tomesh)
	- Jon is exploring some opportunities with Planet Geek

Get together?
	
	- CivicTechTO usually goes out for drinks

### Upcoming Outreach and Workshops

In this sequence over the next few weeks:

	- Build a Mesh Node (Ben, Nick, and whoever wants to help plan)
	- Toronto Internet Infrastructure (Lee, Udit, Ben)
	- Build a Bot (Garry)

### Action Items

- Plan the series of workshops
- Reach out to Wireless Slovenia
- Plan international mesh event in Toronto
- Revise Vision Statement by next weekend (voted to have Curtis draft it, followed by a week of review on the PR)
- Form Code of Conduct Working Group (Lee, Nick, Ben, Leandro, Dennis, David, Curtis, Michael, dcwalk)
- Deploy Vector.im and form virtual space to collaborate with other meshes (Garry, Ben)
- Investigate Kune
- Figure out relationship with non-tech group over next few weeks
- Start building a virtual mesh among all tomesh people, and eventually create a physical mesh taking consideration of people's privacy concerns over exposing home addresses
- Figure out whether we need some legal status and how to acquire it