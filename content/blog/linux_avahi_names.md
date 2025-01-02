---
title: Duplicate `avahi` names and Linux machines"
date: 2025-01-02T11:04:35-05:00
tags: [linux, avahi, home-network]
---

I set up a Mac Mini (2018) running Ubuntu as a home server last year so I could run Plex, Channels, and possibly self-host a couple other applications (looking into bookmarks and ebooks for the moment). Since I don't dabble too deeply in network setup, I didn't want to set up a DNS server (I've read, "It's always DNS" far too many times to want to deal with that), I left the job up to automatic network discovery… what used to be Rendezvous on OS X (now Bonjour), run by mDNS under the hood. On Linux, that service is provided by [`avahi`](https://avahi.org). 

Occasionally, when the Mac Mini restarts, the hostname of the computer gets a `-2` appended to it. In the past, this was caused in Bonjour by the network detecting another instance of the same computer name. I believe this is because DNS changes can take time to propagate through the network, so when Bonjour polls for the availability of a name, another device on the network says, "Hey, I think someone else is using that name.". Restarting the various systems took care of the issue, but it was annoying. On macOS, that problem seems to have disappeared. 

On the Ubuntu system, I noticed I couldn't access the computer at `hostname.local` after a restart. Nosing through the router info, I saw the computer name was now `hostname-2.local`, and navigating to that worked like a charm… but not what I wanted! After loads of searching and restarting just about every system I could find, I stumbled upon [this post at ServerFault](https://serverfault.com/questions/652102/how-to-prevent-avahi-adding-2-to-hostnames) suggesting that the Avahi daemon needed to be restarted. Restarting the daemon with `sudo service avahi-daemon restart` seems to resolve the matter. 

In an effort to make this easier to solve next time, I created a function in my `local.zsh` file with the following:

```zsh
function fix_hostname () {
  # Fix hostname when avahi appends a number after restart
  systemctl restart avahi-daemon.service
  avahi-resolve -a $(hostname -I | cut -d ' ' -f1)
  }
```

The first line restarts the service, the second line grabs the IP address of the system and returns the IP address and hostname of the system. Hopefully having this available will make fixing the problem easier. Since it happens only rarely, I haven't put much thought into automating this task with a `cron` job or something similar. 