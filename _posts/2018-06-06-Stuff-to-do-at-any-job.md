---
title: "Stuff to do at any job, new or old"
categories: sysadmin
author: aaroneg
tags: disaster recovery DR inventory planning not-sucking
---
# Intro
In every IT department and whatever job you do in it - whether it's a job you've done a long time or a new department, there are things you have to do if you want to be able to effectively manage it.

# Gather information
If you've ever been part of a competition like CCDC, you know that the first thing to do is to get an inventory of machines and what they do. Your attackers are certainly going to do that first, and why should you be the only one without information?

The following is a (non comprehensive) list of things I document at a job.

## Initial Critical documentation
[ ] Get a list of all of your servers and workstations and other devices (Sensors, door control systems, etc) and what function they perform. 
[ ] Identify critical infrastructure (including line-of-business applications) and who is responsible for it.
[ ] List out your critical path for what servers/services depend on the others, and the order they should be brought up in case of an emergency like a power outage.
[ ] List out the reverse path to know what should be shut down in what order in case you get enough warning for an outage/emergency
[ ] Gather any existing documentation you can find and preserve it in its current state - it usually is out of date but can provide vital clues

## Network
[ ] List all network devices (firewalls, switches, routers, Wireless access points, etc). Names, IPs, models, firmware revisions)
[ ] Save the configs of all of these devices as your initial reference
[ ] Save these configs in a Git instance also.

## Scripts & Scheduled Tasks
[ ] Discover all scheduled tasks and cron jobs including what accounts are used to run them.
[ ] Discover all scripts tied to those tasks or laying around and just invoked by hand
[ ] Make sure all of those scripts are added to some git instance and that this instance is backed up. Add README files as necessary to document all of these scripts - where you found them, whether they were running as a specific user


This is not a comprehensive list, it's only meant to give you a start. You need to understand and document all of your configuration management systems before you start changing them. 
