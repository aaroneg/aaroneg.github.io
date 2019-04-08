---
title: "2019 SWCCDC Summary"
categories: ccdc
author: aaroneg
tags: swccdc
---

After my friend Taylor wrote a [wonderful summary](https://www.tsmithcreative.com/blog/2019/southwest-ccdc/) of his experience helping to run Southwest CCDC, he suggested that someone from the technical side should do so as well.

Unfortunately, I'm not as clever at graphics or photography or anything of that nature, so you'll just have to settle for this photo of my new buddy, Blue.

![A photo of my new buddy, Blue the Velociraptor]({{ site.baseurl }}/assets/swccdc-2019/blue.png "Blue!")

# SWCCDC
For this year, as I have the last few years, I've volunteered to help build and run the Southeast region of [CCDC](https://southwestccdc.com/whatisccdc/). I've linked a "what is CCDC" article here, so you don't have to search for it yourself.

The short form is that you build a full IT department in about 8 physical pieces of hardware. The students then get the joy of keeping it running and maintaining it while also fending off attacks from a dedicated red team.

It's a lot of things, with a wide focus, and so it is that these students learn a lot about what it's like to actually work in IT. The only real difference is that you will probably do your job for more than two days, and maybe there aren't as many persistent, dedicated attackers.

Aside from keeping the machines they are given and their services online - the students are also asked to do some tasks that simulate as real a business environment and it's needs as we can possibly squeeze into the time allotted.

It's all scored, and while the scoring is outside the scope of my expertise, suffice to say that you can choose to keep a service up or not, or do a task or not, but it's always in your best interest to be careful when considering what choice to make, and before making changes in their environment.

## Scenario

In previous years, we've made up some fake companies for each round of the competition, built their services, and didn't have nearly as much time to write a story line or a scenario. Those efforts came up with some awesome concepts and ideas, and this year we were able to take a different approach, and it turned out to be _delightful_. 

This year, we created a chain of companies, and each layer of the scenario interacted with and informed the next. It was *SO MUCH FUN*.

### Warmup 

Since folks asked us how to practice, this year we created a Warmup round. A few virtual machines combined with a few tasks, with some self-scoring and (if they participated) they could submit the responses to us for some basic scoring and feedback. 

This round was a few hours of work for the students, having just arrived at the law firm of Dewey, Cheatem & Howe. *The Southwest's premier provider of perfectly legitimate legal services.*

At the conclusion of this scenario, the team moved on to their new positions at DCH's crispy new client. 

### Qualifiers

The company for Qualifiers is the awesome, exciting, new, and completely fictional genetics company, CrispyGen. Quals is about 4 hours long, and done remotely so as to allow the greatest opportunity for teams to compete, especially since there's no travel involved and all they have to provide is an internet connection, a space, and a judge. 

At the conclusion of qualifiers, some employees of CrispyGen stampeded off to the next company for the finals.

### Regionals

This is the round that is the most personally satisfying for me, when we get to meet the students that have managed to do well enough in quals to make the trip to the University of Tulsa, right here in beautiful Tulsa, OK. 

This stage involved work for the new and amazing adventure: Triassic Park, newly opened in the stunning yet very remote locale of Isla Fubar, somewhere in the southern Atlantic ocean. 

It is strongly implied, but not canon, that the previous team are now human nuggets for the dinosaurs. Oops. Guess they should have been better at maintaining their electric fences, which is beyond the scope of this post, but well covered in Taylor's post, linked above.

Obviously we took some inspiration from some of our favorite movies when designing the characters, machines, and a bunch of details in the game.

One machine had the same file browser you saw most on the screen from the Jurassic movie, or as near to it as we could find. We also worked in as many other references as were funny or made sense. See Taylor's write-up above for more of the fun aspects. All of the machines were named after dinosaurs, either from a children's movie or just because the name seemed to make sense for the role of the machine. 

Many in-game characters were also from movies, including the infamous Dennis.

## Team Composition

All rounds of the competition each year involve building servers and services designed to teach the students important things about working in IT. Something that would perhaps surprise someone new to IT but not anyone who's spent much time doing the job in real life, is that a successful team does not just involve having a bunch of folks who have immersed themselves into a specific technology enough to know it inside and out. It's certainly helpful to have people like that on your team, but you need generalists who are talented at figuring out new things in a hurry.

You also need folks that have these characteristics, or understand these subjects in no particular order:

* Policy
* Leadership
* Organizing

In real life, you will deal with folks outside your department, and some of them can really ruin your life if you mis-handle them. Among these are accounting, Admins/Assistants, etc. You must do your best to maintain good relationships with the rest of the organization, so that they don't apply the most petty part of their nature to dealings with you.

You also have to apply some basic human skills when working together:

* Respect
* Kindness
* Responding to stress without letting it completely shut you down.

I touch on these things because in some years, I've seen a lot of students struggle with them. It is especially important for each team member to listen attentively when anyone is speaking to them. Do not dismiss or ignore them because of some sexism or other prejudices. They made the team for a reason.  

This year, pretty much every team succeeded at avoiding the worst pitfalls, and I was very proud to see teams working together properly and listening to each other, managing stress and being respectful to each other. 

## Technical

I can hear you now - "Ok but tell me more about the technical stuff - I was promised some technical stuff instead of more repetition from the what is ccdc video, and Taylor's write-up." 

Yes, I get it, and so here we go.

## ~~Dirty tricks~~ Educational Goals and Configurations

First, a note on the machine builds. 

All of these machines are built with a purpose, and include a plethora of horrible applications, or configurations that we have collectively seen throughout our real life work experiences. Sometimes the horrible person who put them in place was us.

To be included in the build, there must be a real educational purpose to the item. In some cases the goal is to prod the student to learn more about an important technology or a methodology they should learn in order to succeed in real life. In others, the lesson is that there is usually a reason the person they're replacing has parted ways with the company, and that might be because they were terrible and left a mess behind for you to clean up. Sorry. It seems mean on it's surface but it is also true and real.

## Windows

I've noticed a trend among CCDC students - oodles of linux knowledge, but a huge deficit for Windows based machines. In previous years we started to introduce Active Directory into the mix in response to this, and now I'm happy to say that almost no team arrives for the competition empty handed on Windows.

### Active Directory

All iterations of our active directory controllers are built using scripts. Automation is key in a task like this, where you have at least 8 domains to build and a very limited time to do it. The only real answer for how to do this is pretty simple - powershell. You can build an entire Windows server environment using only powershell. 

.. Which turns out to be a good thing - both for our build speed and for the students. I really enjoy giving folks a Core windows install. No gui - just a command window. While I do not love Linux, bash, python, etc - I find that no matter what you're doing in life, a CLI is omni-present. And I agree with folks who believe that you should know your job well enough to automate as much of it as possible, and to do that from a command line. 

When I first introduced the concept of a Windows Core install to the students, it was a remote qualifier round. I saw some folks trying to install the GUI back onto the machine. Unfortunately for the students, this was a version of windows that did not include the ability to choose to re-install the GUI. Oops 😈. The educational goals here are:

* Core is very appropriate for a role like an AD controller - it reduces attack surface
* Core is most efficiently operated when you understand powershell. 
* Automation is a thing you should get good at.
* Powershell is the only meaningful way to automate Windows services.

You cannot ever count on the fact that a GUI will always be present, or completely functional -  so learn how to do things the CLI way and you won't be caught off guard when you sit down at one of those systems. Many Microsoft products do not expose all of their configurable options in any GUI built for them. This includes basic server roles like DNS. 

Here are some of the basic items the students were asked to do during the competition that would have benefitted heavily from powershell & automation.

* Creating users
* Massive password resets
* Joining machines to AD _en masse_ 
* various attribute changes covered in the next section.

We also threw in a few tasks relating to group policy, because that's baked into every windows version meant for businesses, despite Microsoft pushing for new management options in more recent versions.

Here are some awful things you can do with group policy that we in fact did:

* Turn all firewalls on
* Allowing all inbound and outbound traffic
* While ignoring all local firewall changes.

Oh dear. While most people caught that the firewalls were allowing all traffic, nobody that I spoke to noticed that all local firewall changes were being honored. So either all traffic was allowed, or none was by the time they noticed that the allow all options were on and set it to block all traffic. The net effect was that nobody was able to successfully open ports on any server that wasn't a domain controller, which has it's own built-in default policy that I didn't muck with. Educational goals here are:

* Group Policy can really ruin your day if you don't understand the policies you have before changing them.
* It can also ruin your day if you DO understand what policies you have, but don't understand how they apply, and in what order
* It can also ruin your day if you make the slightest mistake with it.

In other words, while it's a legacy technology given microsoft's current direction on how to manage windows - you had best get good at it if you intend to be a windows specialist or a generalized systems administrator. 

### Fun New Stuff

This year, I was asked to introduce a horrible new wrinkle: Microsoft Exchange. Yeah. Everyone who's run Exchange on-prem is reading this and shuddering. Super picky, super fragile, and the only real choice for a real enterprise scale mail system outside of Exchange Online. Yes, you can do other mail systems but you are gonna have a worse time. Nothing else has the maturity to handle the needs of big business. 

I was also super short on time to do the work of automating the install since my work life had been exploding and eating all of my time. So I was either going to get the automation part done quickly or spend a few sleepless nights building 8 exchange servers. Yikes. 

As it turns out, this was one of the more time consuming and complex builds I've ever had to get ready (My wonderful friends and colleagues actually did the work of putting the bits on each machine, due to me having duck out early each night to get enough sleep to do my day job)

For those who have never set up an Exchange server, you should now be told that Exchange can scale incredibly well. From one server that does all things and only survives because the mail flow isn't high, to massive, global distribution of dozens or hundreds of servers, each with only one role of Exchange installed. Mailbox servers for storing mail, Hub servers for processing mail as it flows from one place to another, client access servers to do the job of hosting webmail and taking orders from clients, including Outlook and many other mail clients.. 

Suffice to say, it can get super sticky and gross. You can make a career out of designing and building exchange environments, and maintaining them through daily work and upgrades and patching.

This exchange install was all-roles-on-one-server and relatively simple. Simple mail flow, no special frills. Unfortunately you can't start building exchange until AD is up and going, and in the case of our network design this year, the firewall also had to be up and going correctly first. Oh boy. Normally, we can build almost everything in parallel. 

We also sometimes offer the in-game service of 'restoring from backup' the AD controller since it's so central to all services that when (not if) Red team takes it out, you're not out of the game permanently. With exchange we had to offer both, since Exchange stores it's configuration in AD. This didn't go well since the rebuild had to happen in the team room live during the competition because the firewall was between the network segments. Yikes. 

## Create your own lab
I have a sample set of scripts [here](https://github.com/aaroneg/PS-CreateADLabs) if you'd like to see what it takes to automate an AD build.


## Overall
This has to be my favorite year of the competition so far. I got to work closely with some great friends, and made new ones. I'm intensely proud of every team that competed - they all put a lot of heart and a lot of work into it, and it showed. Especially with the amount of wrinkles we built in and the tenacity of the Red team. 

I look forward to next year and being able to up my game so the students have new things to do and new levels of what I hope in hindsight, turns out to be fun for them in. In addition to arming them a little better for their careers in IT or other careers that interact with IT. 

Lastly, I want to thank all of the staff who made the competition work. It takes a small army to put this on, and as we grow the team and get better at putting on the competition year over year, the list gets longer.

This is a security competition, so I'm not naming staff names unless specifically told folks want to be identified. Suffice to say this took a monumental effort and months of time out of each of our lives, and has been worth every moment. I appreciate everyone who made it possible for me to contribute this year while still getting a useable amount of sleep in particular.

-Aaron
