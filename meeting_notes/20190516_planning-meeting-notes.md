---
title: Meeting Notes - May 16, 2019
location: FREE GEEK TORONTO
attendees: 9
date: 2019-05-16
startTime: 18:30
endTime: 21:15
---

# Toronto Mesh Planning Session

2019 May 16th  
FREE GEEK TORONTO

## Attendees
Attendees:  
- **HeavyMetal**  
- **ryan_f**:
- **dasanchez**:  
- **kos**:  
- **makeworld**:   
- **DarkDrgn2k**:   
- **Hank**  
- **Tim**  
- **Jeff**:  


### Toronto Mesh Recap (7:00-7:30)

- **TECH UPDATES**
    - **Prototype Release v0.4 Highlights**
        - Doc for modules in modules.md (moved from README)
        - Notes on how to use cjdns and yggdrasil
        - Profiles available during install time to avoid presenting too many options
        - Yggdrasil officially added
        - YGG IPv6 addresses for all access point clients
        - Bumped IPFS version
        - Mesh point and ad-hoc both work on 2 GHz
        - RPi0 AP works now
        - IPFS works on YGG
        - Contrib module can be set during install
        - Welcome/landing page
        - Patch releases: 0.41 and 0.42
            - hostapd / cjdns DNS addresses
            - patchfoo rolled back to working version
        - ADVERTISE v0.4 RELEASE ON TWITTER! => dasanchez  

    - **Prototype Release v0.5 Roadmap**
        - Modularizing code for .deb packages readiness
        - Being able to select networking protocol (not forcing cjdns)
        - Multiple architectures supported (including x86/x64)
        - IPFS will use less resources
        - hostname will change depending on what platform is being used
        - YGG tunnel
        - Geolocation for pushing that along with the node info
        - Grafana, IPFS, YGG, Prometheus updated
        - Config files
        - MAIN GOAL: PUBLISH TO DEB REPO for improved **USER EXPERIENCE**

- **Org Updates (outreach / talks)**
    - benhylau's workshop facilitation session
    - Workshop highlights (Hank):
        - Modularizing content, if we only want to present one section, that is possible.
        - The workshop is essentially complete after current sprint and will not see further updates, for now.
        - [Workshop repo](https://github.com/tomeshnet/p2p-internet-workshop)
        - Thanks lynx & bennlich
    - **CivicTechTO**
        
        - https://www.youtube.com/watch?v=Qg9-k7tguvI
- **Tools Updates**
    - Upgraded droplets
        - Matrix droplet was upgraded in D.O. after getting overloaded, but it wasn't enough
        - Justin donated VM space for the Matrix and Riot servers
    - Migration of Matrix server
        - Mesh services are now running off proxmox (hypervisor)
        - Script is in the Tools channel (WIP)

### Governance (7:30-8:00)
- Have to be around for at least one cycle (6 months)
- Working group lead roles:
    - Design/branding
        - Hank - "Hard maybe for next cycle"
        - Tim is up for contributing in this area
    - Node tech (New role)
        - Yurko
    - Tools: HeavyMetal -> HeavyMetal
    - Central Org: dasanchez -> Tim
        - Organize meetups and planning sessions
        - Post event details to the tomesh.net website
    - Deployment: Pedro.S ? -> Tim
        - For now, shift emphasis toward _Technical Literacy_ / _Technical Outreach_?
        - Technical advocacy / public service approach.
        - Pop up model for a talk / workshop / seminar
        - Coordinate node deployment efforts
        - Any (experimental) setup needs to be matched up with an appropriate outreach activity
        - Clarify goals in respect of these activities
    - Website: garry -> dasanchez
        - Maintain the tomesh.net website  
        -  Review pull requests to the tomesh.net repo
    - Outreach: benhylau, Tim, Hank -> benhylau, ryan_f, Tim
        - Identify outreach opportunities and share with the rest of the group
        - Drive speaking and workshop events
        - dasanchez will give moderator persmissions to Ryan and Tim
    - Code of Conduct monitor: Hank -> Hank
        - Monitor coc@tomesh.net and meetups to make sure members and attendees are following the Code of Conduct
    - Email monitor: Hank -> Hank
        - Respond to all messages that arrive to hello@tomesh.net address
        - HeavyMetal will add Tim to the hello@tomesh.net list of recipients

### Next Cycle Roadmap (8:00-9:00)

- Meeting Schedule
    - Meet & Greet
        - : No more meet & greets scheduled past planning session
            - : Schedule at least one meeting after the planning session
        - Aug, Sep, Oct: Meet & Greet
        - Nov: Planning session
        - January: Meet & Greet
    - Meeting in July
        - Different space needed, FreeGeek will not be available
        - Seneca, YLabs?
    - Working groups (Update) Sync
        - Removed as its own meeting, will get updates via Mesh Sync, Meet & Greets and Planning sessions (time allowing)
    - Mesh Sync
        - Originally bi-weekly video calls worldwide - more adhoc for the time  being
        - To connect and talk with with mesh people internationally
        - Book times, talk, etc
        - Need people to run them
        - Dante, kos could run weekday evenings in rotation with others

- Outreach Opportunities
    - Content Moderation Symposium:
        - https://contentmoderation.art
        - dasanchez is doing a talk/workshop
        - May 25
    - North York Central Library
        - Talk about decentralization **by us**
        - Cryptography activities afterward **not by us**, done by the library
        - July 6th is the tentative
            - Can change, but will likely be a Saturday afternoon
            - dasanchez and makeworld cannot make that date
            - DarkDrgn2k can come to help with tough questions
            - dasanchez will request July 13 / 20 dates
    - From Ryan - June 29: Multiculturalism + technology celebration @ FreeGeek
        - We're invited, some grant money permitting food service
        -  Multicultural/ Technology themes - (like Picnic 2.0?)
        - Toronto Mesh booth / table - node demos?
                - What are we presenting? Discuss in chat.

- Deployment
    - Set a goal after discussion within the group
    - Decide on how to acheive that goal
    - Temporary deployment testing?
    - Bring together ideas
- Branding
    - Stickers / logo
    - Logo document explaining usage
    - [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/) license?
    - Add note / link to website with license from original creator

- Website
    - dasanchez will drive changes (🧠💩 together with Hank)
    - Focus on documentation/info on mesh concepts

- Node software stack
    - See above: _have_ v0.5 released for next cycle
    - Start Debian package work
    - Make a documented roadmap, put on website with project?

- Documentation
    - Workshop
    - Code repo docs are actively being worked on :white_check_mark: 

### Miscellaneous Notes:

- ThinkPads from 2000's?
- N O D E zine:     - https://n-o-d-e.net/zine/
- [CANARIE](https://www.canarie.ca/)
    - Provides cloud infra to technology groups
- Funding options
    - How would funding/payment be handled (formal procedures/ orgs.)?
- Other Outreach Tasks
    - Yurko will start looking into how to handle organization registrations to North York/Toronto library system
