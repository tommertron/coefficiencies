+++
date = '2024-12-30T12:50:01.409397-05:00'
draft = false
title = 'Site Updating Workflow Update'
+++

So after I created [my post creation workflow](https://coefficiencies.com/posts/site-redesign-now-live/), I realized I’d made a mistake in the  Markdown formatting that I needed to correct, which then made me realize I really needed an efficient way to easily update posts. This made me realize the whole way I was thinking about post creation was kind of broken in the first place and completely re-did it. I’ll break down a bit of the problem and the solution here for posterity.

## Workflow 1
My biggest challenge with post creation was that I wanted to create posts in my writing app of choice, [Ulysses](https://ulysses.app), either from my computer or phone, and quickly publish to the site. The primary challenge is that Ulysses doesn’t support the file / folder structure that Hugo requires. I figured this was easily solvable by exporting the posts (with images if applicable) to a remote folder where I had a script that:

1. Added the required metadata to the post
2. Put it and all the images required into a folder
3. Add to my Hugo site
4. Build it locally
5. Sync the public folder to the site where it’s hosted.

This all happened on an old MacBook Pro that I run as a ‘server’ in my house.

Best practice is to build a Hugo site on its hosting server, but I simply couldn’t get the site to build successfully there. I chalked this up to the hosting server being on Linux, and my dev environment for the site being a Mac. But once I built the site and synced to the hosting server, it all worked, so I figured it would be fine.

So this workflow worked fine until the point that I realized I needed to edit a post. With this method, pretty much the only way I could edit a post was to log onto that remote Mac, update the post, build, and rsync the public folder again. Which, if I were less lazy, I suppose I could have just lived with, but it all felt too clunky regardless.

## Workflow 2
I decided all of this would really be way easier if I relied on GitHub as my ‘source of truth’ so that committing a change to GitHub was essentially when I would consider my post published. I started off by diagramming out the workflow for both post creation and editing.

My initial idea was to modify the above workflow so that it would push the built site to GitHub, then issue a command to the hosting server to pull the built site. But I quickly realized this would still be a challenge for updating posts because I’d have to rely on that MacBook to build the site and push each time I had an edit.

So I started digging into the problem of why the site wouldn’t build on Linux in the first place. It turns out the version of Hugo that I’d installed on the hosting server (via ‘apt’) was woefully out of date. Once I removed it and installed the latest version from Hugo’s GitHub page, it worked! 

This would make things so much easier as I could always just worry about editing the markdown files and images, which are relatively small, and letting the server create the public site.

The last step though was to automate the public site building based on updates to the GitHub workflow. I was initially considering using a service like [IFTTT](https://ifttt.com) to monitor for commits to my GitHub repository, create a file in Dropbox, which would sync to my local Mac, which would trigger a script to send SSH commands to the local server. This probably would have worked, but just felt too clunky for my liking.

It turns out, GitHub already has tools for this kind of thing, with [GitHub Actions](https://github.com/features/actions). GitHub actions are little workflows you can configure to run automatically each time there is a new commit to your repository. And GitHub even lets you store your private SSH keys as secrets, which GitHub Actions can reference. This means I can put one of the SSH keys that the remote server accepts in GitHub, and let GitHub actually issue the commands to the remote server to pull the latest source and then rebuild the site.

So now I have a workflow where GitHub is at the source. All I have to do is make sure new posts or updates to posts make their way to GitHub and the site will be automatically updated!