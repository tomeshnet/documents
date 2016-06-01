---
title: Meeting Notes - May 31, 2016
location: Civic Tech TO, The DMZ
attendees: 4
date: 2016-05-31
startTime: 19:30
endTime: 21:00
---

# Agenda

0. Intros
1. Potential project with the Government of Canada Innovations
2. Wekan and Rocket.Chat deployment update
3. Status update on Maker demo and satellite

# Notes

- General tech stack overview of the [Pi 2 prototype](https://github.com/tomeshnet/prototype-cjdns-pi2)
- Open question: How can we build a sustainable network?
- Reaffirming transparent process documentation (e.g. Github documents, prototype documentation)
- Connect with Government of Canada Innovation contact this week from Ethereum meetup
  - Initial meet and greet
  - Possible collaboration
- [USB Dead Drops](https://deaddrops.com/) by Aram Bartholl
- Interesting project: [Facebook Tunnel Project](https://github.com/matiasinsaurralde/facebook-tunnel)
- TOMesh will be present for June 6 hackday at Ryerson SLC with Civic Tech

## Infrastructure: Rocket.Chat and Wekan Deployment

- Deployment issues on the VPS
  - Most likely Node version dependencies: Build script could be using an old version of Node
  - There's no Node version management on the server at the moment
  - Might opt for a manual build of Wekan
- Digital Ocean is the next choice for deploying Wekan and Rocket.Chat if there are continued issues
- Possible feature (post-deploy): A chat bot for Rocket.Chat
  - A bot that can parse chat and reference a source document or group subject matter
  - Google's Natural Language processing, [Syntaxnet](http://googleresearch.blogspot.ca/2016/05/announcing-syntaxnet-worlds-most.html)
  - Not known if it's a self-hosted service or a Google hosted API

## Pi 2 Prototype Update

- Demo of current implimentation with setup scripts from [repo](https://github.com/tomeshnet/prototype-cjdns-pi2) with CJDNS
- Hardware requirements for Maker Festival (so far):
  - Raspberry Pi 2: 6 (Already have 4)
  - TP-Link WN722N: 6 (Already have 6)
  - USB Power Adapters (Micro): 6
  - Webcams: 2–4
  - Webcams that are compatible with the Pi (Raspbian ready. We can look at the native Pi camera)
- Goals for June 6:
  - Confirm prototype implimentation on Pi 3
  - Get video link working with webcams
