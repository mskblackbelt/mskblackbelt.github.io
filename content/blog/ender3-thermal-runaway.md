---
title: "Thermal Runaway error on Creality Ender 3 Neo"
date: 2023-02-05
author: Dustin Wheeler
tags: [3d-printer, TIL]
---

Just before Christmas, I purchased a Creality Ender 3 Neo (v1) printer on discount. Up to now, I've been working with a Monoprice Select Mini Pro (purchased at the start of the pandemic so I could work on 3D modeling projects at home…). That never really took off… partly because the Monoprice machine was soooo difficult to work with that larger prints were impossible. In addition, the bed size on the machine was 6" x 6", pretty small for a lot of projects. 

Fast forward to this Christmas, I wanted to make some 3D printed projects for gifts and needed to work on some of them at home. I saw a good price on the Ender 3 Neo v1[^fn1] and decided to grab it. After some assembly, I had a _massive_ machine on my desk (compared to the Monoprice one), but it had a decent sized glass build plate, auto bed leveling, and the promise of better print quality. I made one or two test prints to check the bed adhesion and leveling with success. Then I tried a longer print (can't even recall what). It looked like everything was going well after 10 minutes, so I went downstairs to grab some dinner. After a few minutes, I hear a _raucous_ beep coming from the printer. When I checked on the screen, it was complaining about a "Thermal Runaway". 

I figured this was a one-time issue, so I resliced the print, sent it back over to the machine, and started again. Again, after about 30 minutes, the printer gave off an awful beep and complained about a thermal runaway. This happened a number of times, so I gave up for a bit. I did a bit of research online and a number of posts pointed me toward PID tuning, loose screws on the thermocouple, and suggestions to replace the firmware with Marlin. I checked the screws (tight, no issue) and decided it wasn't worth messing with PID tuning if I was going to replace the firmware… by this time, it was late and I had family coming soon, so I turned off the printer and left it to gather dust for a few weeks. 

This afternoon, I decided to try to make some progress on the matter. Before pulling the trigger on new firmware,[^fn2] I did a bit more reading on the matter on some Stackexchange and Reddit posts. One [post in particular][reddit-soln] suggested the most _ridiculous_ solution… ___obviously___ this couldn't possibly the the answer, right!? If you didn't click through, the poster suggested checking to make sure the power supply was set to the right voltage (115V/230V). The only reason this felt ridiculous was that I had to select my voltage and plug locale for the printer on checkout, so I assumed that those values would be correctly configured for my region. _Turns out,_ I was wrong. My power supply was set to 115V. A quick flip of the switch and I'm back in business.[^fn3]


[^fn1]: Creality has the _worst_ model distinctions… well, except for Monoprice, Flashforge, and every other inexpensive 3D printer manufacturer
[^fn2]: I might still do this just because I like some of the features enabled with Marlin. 
[^fn3]: Hopefully. I have to actually run one of those prints now, setting it up as soon as this post is finished. 

[reddit-soln]: https://www.reddit.com/r/ender3v2/comments/m8k5ig/comment/ilwo4sg/?utm_source=share&utm_medium=web2x&context=3