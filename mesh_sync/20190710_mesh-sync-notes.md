Mesh Sync
=========

📍 https://appear.in/tomeshnet  
📅 Wednesday, July 10, 2019

| Timezone | Start time |
|:---------|:-----------|
| EST      | `07:00 pm` |

## What is this?

Biweekly open calls to sync up on topics relating to the global Community Network movement. The hours are selected to make it possible for parties of different timezones to attend.

Anyone may propose a topic on [this open-edit pad](https://hackmd.io/HSOK15u7TnS6Oz1RH0McGg), taking one of five session timeslots by putting yourself as _Facilitator_ and filling the corresponding [_Agenda_](#Agenda) section. You can see previous meeting notes on [tomeshnet/documents/mesh_sync](https://github.com/tomeshnet/documents/tree/master/mesh_sync) to get an idea of what type of topics have been discussed in the past.

Please scope your session within a 20 minute time block. If more time is needed, it is probably best to use the 20 minutes to give an overview, then schedule separate meetings with interested parties. The hope is that these standing hours can be well attended and everyone participating gets a general idea of global initiatives relating to the Community Network movement :satellite:

## Attending

📝 This person moves meeting notes to GitHub and resets the pad:
- 

👥 Please add your name to this list if attending:
- @Darkdrgn2k
- @Hurricos 
- @dasanchez
- @timtor

## Agenda

No preset agenda - Free Form

#### Notes

- Quick conversation about "Bell Fibe" ("FTTN") vs "Bell Fiber" ("FTTH")
    - Gigabit speeds seem to only be attainable during Bell's speed test
    - Rock64 connected to 1gbps only does ~500mhz on "speedtest-cli"
    - iperf3 to vps node only hits ~110-150
    
- Discussion Around outreach projects to "ALT" isps
    - Teksavvy, Beanfield, swift
    - Need to have a more concrete concept to present
- State-of-the-art protocols vs low-resource ones
    - CJDNS and YGG may be working against us
    - Tons of computing power required because encryption
    - Babel may not have addressing and encryption, but it works
-  DWEB apps not "mesh friendly"
    - lacks IPV6 support
    - Built for "traditional" infustructure
    - Example - IPFS not knowing topology 
        - Doesnt care who they take the data from from a topoplgy perspective
        - ISPs carry the backhaul burden
        - IE Level 3 probably only uses a small % of their capacity
        - Meshes have to shoulder that burden
    - Imagining a "caching" node for content on the roof of a Multi Dwelling Unit
        - Encryption makes caching impossible
        - Suggestion - perhaps homogeneous encryption has a place here
- Prototype and SSB for TPL 
    - SSB does listen for IPv6 announcement packets :( 
    - Work around are
        - Invite to ipv6 cjdns peer
        - Add ipv4 address to wlan0 interface to bypass cjdns ipv6 address
- Burlington, VT project for [The Ramble](https://theramble.org/) - MESH ice cast audio stream
    - Long buffer to allow for roaming
    - Pis runing 5v batteries
    - MR16 mesh

#### Important things for future Syncs
- Taking notes
- Making the output freely available
  - That is to say, organize and publish the notes that come out of it, as before
- Advertise beforehand
    - Decide on time earlier
- Improve chat
  - Jitsi just wasn't working - would Mumble be better? What type of chat would be better?
    - Suggestion: Multi-modal chat (attendees can talk chat in a voice chatroom, and a stream of the chat is published so people can involve themselves via a text chatroom)
    
