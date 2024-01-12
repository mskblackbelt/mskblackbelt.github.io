---
title: "Creating a network share on Windows 7 (Pro) accessible from Windows NT 4.0"
date: 2023-04-28T15:38:56-04:00
tags: [TIL, networking, Windows]
draft: true
---

A colleague and I set out to rid ourselves of floppy disks. Several of the control computers in the teaching labs are pretty old, still running Windows NT 4.0. Because of software and hardware requirements, OS upgrades are out of the question, and USB and CD-RW support are non-existent in NT. But all the machines are equipped with ethernet, so we decided to set up a small LAN.  The trickiest part of the process was getting to the realization that NT 4.0 didn't come with the TCP/IP stack installed by default… we had to pull out the NT install discs and have Windows install that stack before we could communicate with other machines. What a throwback, I'd forgotten (and wasn't working deeply with networks at the time) that there were versions of Windows without TCP/IP.  