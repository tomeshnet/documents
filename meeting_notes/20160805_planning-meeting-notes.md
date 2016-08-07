---
title: Planning Meeting Notes - August 5, 2016
location: HackLab.TO
attendees: 14
date: 2016-08-05
startTime: 19:00
endTime: 23:30
---

# History, Development, What We've Learned So Far

BEN: I got interested in distributed networks and how mesh can do that. Not from networking or security background, a lot of learning along way.

Discovered Civic Tech TO. Good place to meet people who are interested. Met Gabe, Dawn, Garry, Curtis, etc.

We figured out what the problems were, what needs to be resolved. Talking with other mesh networks.

There are sustained mesh like Barcelona, etc, but North America doesn't have sustainable mesh. They fizzle out. What is the magic ingredient?

Can't just focus on building the tech. Must grow the community and distribute the knowledge on how tomaintain it.  Must scale community in line with the mesh.
Technical literacy education modules.

Tech platform -> Raspberry Pi. Initial idea to flash routers, but they are becoming increasingly locked down. Interested in a platform that is a lot more flexible. Distributed networks, distributed applications.

Focus on security and privacy at the protocol layer. Trying to do those things at application layer -> people do it wrong. Not advocating neglecting security at the app layer. And IP allocation decentralized.

Platform based on Raspbian. Flash SD card and run a line of code and the Pi will reboot and talk to one another. Can just connect through SSH to node remotely, end-to-end encrypted.

The mesh topology and the tech stack has the right attributes, but don't know if it can scale. Hyperboria has 700+ nodes globally, has been working, but nobody has deployed local network with cjdns that has worked at a large scale.

NICK: Wireless Slovenia uses cjdns and has 1000+ nodes. Some scalability issues but they're doing it.

BEN: Really? Wow great, didn't know, will look at that. Make a card on Wekan.

# State of tomesh Now

## Maker Festival

Outreach where we built a game board. Learned what people care about.

UDIT: One thing we realized early on was that we had a hard time connecting with people about why this is important and what we are trying to do.  Brainstormed and came up with a game to showcase what the problems are with centralized systems. In the board game, you connect parts of city and it would bring down parts of your system and you had to reconnect, demonstrating the faults of centralized system. Kids interested. Using a Raspberry Pi instead of a modem was great to get people involved on a lower level than just talking about mesh itself.

## HOPE xi – N.Y.

BEN: Hackers On Planet Earth is a conference like Chaos Computing Club. Discussed what does tech mean to society?

Being aware of the problems and potential, and see the social value, consider that when we build the things we build.

Spent lots of time with NYC mesh guys. Oakland sudomesh people were there. A lot of people agreeing that we need a distributed ownerless last-mile network and a step to having free access to info where interests are aligned with people who use it and not the telecoms.

On hardware side we want open platforms, but also want them to be cheap.
This is part of building mesh tech in Toronto, but want to be portable to other countries. Frequency bands may differ in other countries. Frequency agnostic system is one goal. Build the right levels of abstractions.

LEE & MICHAEL: Looked into SDR? Do we want to claim more parts of the spectrum? Like UHF? Is that possible?

[Discussions]

UDIT: Talked about using 900 MHz, TV Whitespace.

MICHAEL: Packets with shortwave?

BEN: In NY, we discussed using 900 MHz for VOIP, use WiFi exclusively for other data.

LEE: Use 900 MHz for node handling? [Dynamic sharing of routing information.]

NICK: Most nodes will be stationary.

BEN: Use mesh as last-mile, cellphones to exit to the Internet from home ISP plan. So many ways this can go.

GARRY: Ben, you mentioned NYC...

BEN: Various initiatives in NYC. Group that's working with BATMAN, but also initiatives to move away from BATMAN because there are issues and there isn't a lot of in-house expertise with deep knowledge of BATMAN. Install process is painful. You have to downgrade AirOS and flash OpenWrt. Hard to self set up. Some people want to switch to cjdns.

We don't want to set up for people, it's unsustainable and against our principles of user ownership. [Getting a node working shouldn't be rocket science.]

The issue of Internet access has come up many times. We have a plan for this, from a discussion in NY. [We have the discussions summarized here](https://github.com/tomeshnet/mesh-isp). Anyone can be an ISP, selling upstream bandwidth to the Internet downstream to clients. Need minimal knowledge about clients to do this. You can do a Bitcoin transaction to sell portion of your upstream bandwidth to others. This is exactly like buying a VPN with Bitcoins.

DAWN: Lots of interest from other mesh groups and people involved in mesh projects. In near future lets get everyone in the same place. International event and invite everyone to come to Toronto.

BEN: First, have a virtual space for mesh people to communicate. [Vector](https://vector.im) and [Matrix Homeserver](http://matrix.org), an open federated chat app and protocol. Instead of being tied to Slack. We generally like to run things ourselves instead ofdepending on centralized services.

BEN: Questions?

NICK: Do we have nodes?

BEN: Yes, 3 in my apartment.

LEE: Do they each have an Internet egress point?

BEN: We haven't moved them far enough to test routing. Every node was connected to every other node.

LEE: What about [...]

BEN: Actually, we tested them in Bahen Center in a straight line. And they worked. But we need to go to a park and test.

NICK: HackLab has roof access. Line-of-sight to places.

BEN: Recently learned that line-of-sight doesn't necessarily have to be line-of-sight. [See Fresnel zone](https://en.wikipedia.org/wiki/Fresnel_zone).

MICHAEL: Question about privacy and encryption. Encryption at header level?

BEN: No, it's not anonymous, but you can run TOR over cjdns. Anonymity is hugely inefficient. With cjdns you get security but not anonymity. When you start a node you generate a public and private key. The public key is used to derive an IP, creating an identity that doesn’t depend on central authority. When you speak to a node you are doing source routing, nodes are constantly discovering paths. You decide your path to the end node. Use keys to encrypt packet to negotiate a shared secret with the destination node, then encrypt the communication with that shared secret. Throw away the shared secret after that session. This ensures forward secrecy.

MICHAEL: That's really important! [Gave example on how some previously encrypted messages were decrypted after the key got exposed.]

# Vision Statement

GARRY: Vision statement is present on website, and there has been discussion about revising it. Does it still hold true? There is a Github pull request for some changes.

BEN: Last time we talked about this we agreed we all cared about these things but not necessarily in that order. Presentation of vision impacts how it relates to funding, etc. Also wording, it was confusing for some people to read this.

DAWN: Part of it was at that time we didn't have a secured path for funding and didn't have a deployment project for defining it. So we were trying to figure it out without knowing where it was going.

BEN: Initiate a vote on per item basis in the Vision.

NICK: Curious about whether tomesh as an organization has put thought into human dynamics of this. Some people might be more interest in the tech and don't care about being nice to each other. Do we handle that?

DAWN: Yes. We have a Code of Conduct. Held off on pushing things through. Having *enforceable* Code of Conduct is important.

BEN: Difficult to enforce a code of conduct in a distributed system. Easy to establish but hard to enforce.

DAWN: Let's make a working group on some of these issues to work it through since we wont have time to do
it all today.

**CoC Workgroup**: Lee, Nick, Ben, Leandro, Dennis, David, Curtis, Dawn, Michael

MICHAEL: I'm concenrned about how people can screw with the system, malicious intent, etc.

BEN: Network level abuse need to be handled at the protocol level.

CURTIS to NICK: I liked your comment about community.

NICK: Makerspaces have a culture of being good to each other. But if you don't have that in place things can get out of hand. It'simportant to establish that "being good to each other" culture, get it entrenched early on. If you don't do it early there's no way to recover.

BEN: The exact wording, we'll put something up this weekend on the Slack channel. Try to solidify it and have something by next weekend.

CURTIS: Let's write it in such a way so that each keyword is same tense, or... you know, nouns vs. verbs, etc.

BEN: Great idea Curtis. You should do it :)

**VOTE**: For Curtis to write revised Vision Statement.

# Non-tech WiFi Research Group Update

LEANDRO: Intro about efforts so far. Considering target communities, weighing need for something like this in community, how well it satisfies tomesh's needs for test deployment (we haven't really talked about this with tech group), what local resources available, community connections, symbiotic initiatives, funding. TCH looks good, especially with Nahum's connections in such communities and programs happening there. Researching where we have the best access to go in and actually do something there. Orton Park has most meat on bones in terms of access for us, but also looking into Swansea (High park), Firgrove (Jane/Finch), Kensington Market.

Starting to discuss door-to-door research with residents and other community members to gather data. What do people in these communities lack and desire? Met Toronto Star Data Lab director and in contact with ACORN, who together have experience doing door-to-door surveying and mapping maintenance issues. Could be very useful for us in terms of how to interact with these communities, how to create consistent and useful questionnaires, how to compile and analyze data effectively and efficiently with minimal staff.

We've been talking about developing Maker culture in these communities to increase technical literacy required for sustainable mesh deployment.  Have discussed even creating our own Maker spaces or working with other orgs to do it. Evolving Maker programs to include networking and Raspberry Pi's, mesh concepts, etc. [This is one point where ideas and pre-requisites for tomesh deployment divergefrom main goals.] Gathering local support and recognition of mesh in communities.

UDIT: [Read Nahum's outreach doc]

DAWN: Capacity building, we need to figure out how much to do in the beginning. How much of the literacy component we are prepared to do.

NICK: How much of this stuff is a natural growth that can come out of this? There's an organic aspect out of growing this project.

BEN: I think a lot of people are interested in low-cost internet. But the mesh network is not there yet. What throughput can we get out of tunnelling through cjdns? Hard to commit to a timeline. Eventually we may have an [Airbnb for ISP](https://github.com/tomeshnet/mesh-isp), but it's hard to, at this moment, plan a low-cost access project around.

UDIT: Low cost access is not the sole focus of tomesh. There are other focus points, like security and decentralization. We shouldn't just start providing low-cost access or change direction to do that. We should make sure we have the security aspect, etc, ready from the get-go.

LEE: Removing barriers to access as the on-ramp. The goal is always to make things a little bit more fair so everyone can play. Cost aspect was a piece of that, but so was education. If I can get grandma on Linux and her box isn't owned,that's her barrier to access removed. If you make one a subset of the other it's easier to figure out.

UDIT: But let's not sacrifice the security aspect to get the other happening.

BEN: It's not just cost. We've been forcing telecoms to give up some of their infrastructure, coffee shop WiFi, etc., but it hasn't solved the problem because we didn't change the ownership model. We need to change the ownership model. We [who have Internet access] don't go to the library to loan out a Raspberry Pi to go online. Why should we expect anyone to? We should all have the same level of access.

UNKNOWN: Do we even need Internet on tomesh?

BEN: Yes/no, maybe.

MICHAEL: [Missed this comment.] Developers developers developers :)

BEN: We don't necessarily need just developers. Because the community are the developers. Everyone can build something. But people have different interests in what to build.

NICK: On creating services on the mesh itself, I've looked into this problem. And how they achieve [...] will sound super corporate but hang with me... Number one barrier to adoption is what are people already doing and how do you get them to do it on the mesh. Going to challenged communities, kids go to McDonalds because they don't get kicked out. That forum good for VOIP, cat pics, piracy, whatever. But if it doesn't have wider Internet and access to what people really need, they will not adopt.

DENNIS: I'm interested [in local in-mesh use cases] because if you want a tool, like a hammer, you will get the closest tool to you. The Internet is local, sharing economy. If we can make [...] we have a network for everyone to be able to find a service or product and should be able to use the mesh to findt hat.

NICK: That's an awesome use case and it's important to use the most local infrastructure possible, but how can you connect people to the community better than Facebook, etc., and how does mesh network itself enable that.

BEN: Your idea about local sharing economy is one of many local services that can be run on mesh network. The technology doesn't care what you do. Just serve it over the mesh. Then you have service over Internet or whatever, you can also serve over the mesh.

Long-term it's not about gatewaying to the Internet. It's about pulling the Internet into the mesh network.

Just put antenna on roof and done. [You are now providing the same service over the local mesh.] ISP running on mesh is also one of the services.

MICHAEL: Look into use cases where using mesh can directly help. i.e. industrial automation. But industry is hesitant about moving toward IoT.

UDIT: Community-owned infrastructure to connect up hardware across the city.

MICHAEL: Use case is about creating a mesh network and we all have houses and community and sitting in the same room. Hey, I have a house can we make a mesh?

BEN: Let's build a virtual mesh over IP.

CURTIS: Lets make a map of where we are.

**TODO**: Build an area map of where people involved in tomesh live and feasibility of making a "tomesh Team Mesh". Concerns about security and privacy of this personal information (addresses).

BEN: Back to the identity crisis the non-tech group is having...

**VOTE**: Bring these things to the next non-tech group and figure out what they want to accomplish. Bring it back to the general tomesh group and have as an agenda point for next meeting where the two groups fit.

# Tools and Practices

BEN: Add Vector.im to list?

Talk about choices about tools used. Open-source and decentralized. Information structures should not be on other people's computers. Open-source, data ownership, facilitate an interaction that is public and not closed participation. Nobody in charge of managing accounts. Github does that because of forking and pull request features. International groups able to copy and adopt and adapt information according to relevancy to them, e.g. India might drop some aspects that don't apply, but adopt existing material from us.

[Introduced existing tools like Github and Wekan.]

LEANDRO: All about [Kune](https://kune.ourproject.org) as a platform.
Similar to Crabgrass, a sharing and collaboration tool with various types of content, tools, features. But many strengths over Crabgrass. Run your own installation on your servers. Extensible using WRT to change whole software or anyone can use Java/Python to easily create apps and bots. (People decide what plugins they want to use individually). Uses single-page dynamic content like Gmail and Twitter rather than static page PHP where browser has to load entirely new page to navigate. All documents and tools are *Waves*. Waves are abandoned Google Wave product that is now open/libre. Wave is a document that can be anything, e.g. a wiki or a calendar or voting poll or video or text document. Kune creates some default profiles and interactions for waves suitable as common and familiar tools and puts them all in one place. Objective is to replace centralized, single purpose services like Gmail, Twitter, Google Docs, IM, Wikipedia, Youtube, etc., with all-in-one dynamic, libre, federated product you control, and do in such a way that anyone can pick up and use intuitively. Also contains chat that is compatible with Gmail Chat and other apps. If you have account on one Kune server you can interact with content and users on any other Kune installation. Basically, it's a beautiful thing... on paper. None of us has explored it yet. I just read all the documentation and FAQs, etc., about it.

**TODO**: Leandro to explore Kune by creating account on Kune.cc and others should too. If there's a positive feedback, especially in comparison to Crabgrass and in regard to ease of managing our own installation on local servers.

MICHAEL: Build automation?

BEN: Nothing to CI (continuous integration) build at the moment. Just simple install scripts we have, on top of larger projects like cjdns that is already on build automation.

GARRY: We agree there are no problems about current tools?

LEANDRO: I have a problem. Usability on a grand scope. Not useable at all. Those who built it over 6 months know what's going on and comfortable with tools and organization. Others of us are completely lost or frustrated and just getting by.

LEE: I have a server if you want to host tomesh tools on a server where you have physical access.

BEN: Yes, possible. Currently hosted on Digital Ocean since it provides the uptime we need.

If you develop something, you are [responsible for documenting it](https://github.com/tomeshnet/documents/tree/master/service_setup). Don't have central points of failure. If you have something that needs authenticated access, share access with at least a couple of people so if you disappear it doesn't get lost or become unusable. Don't share password. Make multiple admin accounts.

# Logo

BEN: Just do it please! Someone?

[Leandro: I didn't mention this because we moved on too quickly and I was taking notes, but branding is a very important thing. It communicates everything about you, even a "feeling" that people take away when exposed.  There are groups that can help develop the identity and image of any initiative according to their needs to very effectively deliver ideas with heavy and memorable impact. The logo, the name, the colours, even vision statements. It does matter. It's not about corporate tactics. It's about human psychology, science, and smart communication.]

# Website

LEANDRO: Wiki intro with what is mesh, links for further info. Then a blog page of what's going on. Content from collaboration, progress, discussion on Crabgrass, Kune.

MICHAEL: Landing pages to get people up to speed about what we're about. Some other page more like a wiki to give more info.

[Showed our existing website and its current features.]

UDIT: In-progress tasks reflected on website?

BEN: No, link to Wekan. It's publicly readable. Write access requires authorization. [A few people here are admins who can send invites.]

GARRY: Meeting notes should be kept for all meetings. Made available to everyone. Current process is to write on a Riseup Pad, then transfer to [this Github repo](https://github.com/tomeshnet/documents/tree/master/meeting_notes).

# [Mesh Deployment section will be added shortly]