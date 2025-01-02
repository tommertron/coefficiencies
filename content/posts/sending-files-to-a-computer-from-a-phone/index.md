+++
date = '2025-01-02T13:44:26.278904-05:00'
draft = false
title = 'Sending Files To a Computer from a Phone'
+++


My [semi recent](https://coefficiencies.com/posts/site-updating-workflow-update/) publishing workflow for this site initially relied on iCloud Drive to send completed posts from Ulysses (on my phone) to a Mac I have at home to process the files and publish to this blog.

This worked to a point but I’ve found that iCloud Drive is not always the fastest or most reliable syncing service. I was finding that a post that I’d send to iCloud Drive wouldn’t be picked up by my Mac server unless I logged in and sometimes restarted iCloud Drive. This was not ideal as I really wanted to minimize the time that a post would be live after I published it.

I initially thought I could try Dropbox, which is a more reliable sync service, but I didn’t like the overhead of having to run Dropbox, and it’s also a little hit or miss what it actually decides to download locally these days.

I wanted to figure out a way to send a file **directly** to my Mac. I have set up SSH access to my Mac, which sort of gives you SFTP access for free, so I figured this would be a viable route. Shortcuts allows you to send SSH commands (and even lets you set up its own SSH keys that you can share with your target device) but alas, I couldn’t figure out how to take an input into a Shortcut and get that into the SSH command to send a file. I tried a few different ways and ended up hitting a wall.

So I searched around for an SFTP/SSH client for the iPhone and stumbled upon [Secure ShellFish](https://secureshellfish.app/) which not only has a nice SFTP / SSH terminal client, but also integrates with Shortcuts, allowing you to upload a file from a Shortcut. 

So I ended up making a little shortcut that would export a file, then use Secure ShellFish to upload the file. I tried it and it worked like a charm! It’s so nice to see a file basically **instantly** show up on my Mac after I run this Shortcut. Of course, this is all made much easier by the fact that I have [TailScale](https://tailscale.com) deployed to my Mac and my iPhone, so I can connect to my Mac securely from anywhere. Did I mention how much I love Tailscale? 

Incidentally, Secure ShellFish is made by the same developer as [Working Copy](https://workingcopy.app/), an excellent GitHub / Git interface that I’ve been using to edit posts for this site. I recommend checking both of them out!
