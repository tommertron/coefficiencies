---
title: "(Another) Update to My Publishing Workflow"
date: 2025-01-17T14:36:01+08:00
tags: [""]
categories: [""]
draft: false
---

At some point I'll actually get around to writing about, you know, topics again, and not just futzing around with how I publish to the site. But futzing is so fun! So I'm just kind of leaning into that right now, so here I go with another workflow update post.

Anyway, my [previous update](https://coefficiencies.com/posts/site-updating-workflow-update/) relied on Ulysses as the core of my writing flow, but because Ulysses didn't support publishing to a Hugo site natively, I had to upload files from it to a server I have at home which would process them. This worked... fine. But felt kind of clunky to me. And since my publishing workflow basically revolves around committing things to my GitHub repository for the site, I can publish to the site anywhere I can publish to GitHub. I also wanted to make something that was a bit more iPad centric, since I'm really digging using my new [iPad mini](https://coefficiencies.com/posts/i-got-an-ipad-mini/) with a keyboard for writing.

I'd discovered the great app [Working Copy](https://workingcopy.app/) for iPhone and iPad, which would let me pull my repo down from GitHub, edit files, and push back which would then update the site. It has a built-in editor, which is Markdown-friendly, but it's not exactly a great writing environment. Digging around a bit (okay, fine, asking ChatGPT) I realized that you can configure Working Copy to show up as a file source in iOS files, and any app that can access iOS files (of which there are many) can edit the repo that Working Copy pulls down. This opened up a world of possibilities!

I had previously purchased the Markdown editor 1Writer, which you can point to any iOS Files folder and create and edit Markdown files, and also supports inserting images into folders. So I could edit posts there, add any images, then hop back into Working Copy which will see all the changes made, and then commit and push updates to GitHub.

This was a nice solution in some regards, but I didn't want to have to manually add the frontmatter that Hugo requires in your Markdown files to generate pages properly. I thought about using iOS Shortcuts to do this, but then realized I could turn to one of my all-time favourite apps: [Drafts](https://getdrafts.com/)!

I won't do a full overview of Drafts here. But essentially the idea with drafts is it always defaults to a new text file when you open it. This is so that you can quickly jot down an idea you have without having to worry about creating a file, naming it, etc. I still have an ingrained habit to 'start' any text based idea in Drafts and then figure out what to do with it later. So it felt like a great spot to start blog posts. I could jot an idea down, then come back to it later to finish writing and posting and whatnot. Drafts itself is a very nice, customizable Markdown editor in its own right, with the caveat that it doesn't support images. 

So I was able to modify an existing action in the Drafts Directory for creating a Hugo post for my publishing workflow. Basically, once I finish writing the post in Drafts, I run an action to insert the frontmatter automatically (getting the title from the first line of the draft), then creating a folder in my site's repo (courtesy of Working Copy's Files integration) with a web-friendly name, and the article as an md file in there. From there, if I have any images to add, I could either do so in 1Writer or Working Copy directly, then commit and push to publish. Voila! 

The only thing I'm finding kinda clunky right now is the many steps it takes to add the files to my commit, commit, then publish. I think my next step will be exploring whether I can create an iOS Shortcut with Working Copy that just adds all new files, commits, and pushes in one step. So I can just hit a "Publish" button in my iPad that will publish all outstanding posts. Stay tuned I guess? 