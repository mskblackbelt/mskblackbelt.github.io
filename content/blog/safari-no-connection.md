---
title: "Safari No Connection"
date: 2023-02-22T14:44:53-05:00
tags: [Safari, networking, iCloud Private Relay]
---

I just spent the past 45 minutes trying to troubleshoot an internet connection problem on my work computers… While trying to set up Tapbots new Mastodon client [Ivory][ivory], I couldn't get the authentication page to load in Safari. My campus connection periodically experiences issues due to any number of things: campus network problems, campus IT problems, campus IT blocking my local router, problems with my local router,[^fn2] etc. In fact, I've been experiencing periodic issues all day. 

[^fn2]: Uncommon, and usually fixed with a reboot.
[ivory]: https://tapbots.com/ivory

I noticed that the Mastodon authentication page was having issues loading… because it's an auth page, Safari won't seem to let you copy the URL.[^fn1] in an early attempt to troubleshoot, I tried to load [Down for Everyone or Just Me](www.downforeveryoneorjustme.com), but that also failed to load. I would have suspected my internet connection itself except that I was in the middle of an iMessage conversation with my wife and Apple Music was streaming without interruption. 

Lately, I've been running [Orion][orion] as my main browser, so I haven't been thinking much about my Safari setup. An odd observation I had was that pages were loading in Orion just fine, suggesting that the network and DNS[^fn3] weren't to blame. My next thought was to start disabling as many extensions, apps, etc. as I could (_all_ Safari extensions, my software firewall, assorted background services…). None of this had any effect. Finally, as I was poking through the Safari preferences, I noticed a little box under the Privacy pane for "Hide IP Address" with a pulldown menu for "from Trackers Only" and "from Trackers and Websites". If you're not familiar with this box, it's tied into Apple's [iCloud Private Relay][icloud-relay] service, which promises to "protect your privacy when you browse the web in Safari."

[^fn1]: My initial thought when Safari was having issues was to copy the URL and paste it into Orion. 
[^fn3]: As I've learned from IT experts on the internet, it's _always_ DNS!
[orion]: https://browser.orion.com
[icloud-relay]: https://support.apple.com/en-us/HT212614

It seems my campus network is incompatible with the Private Relay service though it works if I switch to "from Trackers Only". Maybe it's also broken this way, but the break is just localized to tracker loading, and that's a happy side effect if true. 

So here's my long story about how iCloud Private Relay is still some funny tweaks on technology and the efforts to elude mass data surveillance result in highly inconvenient situations… so hooray capitalism!

