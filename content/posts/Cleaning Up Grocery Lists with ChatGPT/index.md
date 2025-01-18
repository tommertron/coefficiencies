---
title: "Cleaning Up Grocery Lists with ChatGPT"
date: 2025-01-18T15:18:57+08:00
tags: [""]
categories: [""]
draft: false
---

I'm not a frequent cook in our household, but I do like to collect recipes that I come across or keep old favourites that I want to come back to using the great recipe manager [Mela](https://mela.recipes/) for iOS and iPad. Mela excels at collecting recipes from various sources, parsing out the ingredients and directions and relevant pictures, and giving it to you in a nice clean format without ads or introductory posts. When it's time to cook, it presents your directions step-by-step in nice, large text. It also has a very clever and cool feature that detects times in the directions, and will let you click on that time to start a timer. And, of course, it lets you create grocery lists based on recipes to help you plan, and even lets you push the items into iOS Reminders. Which, ostensibly, is great!

The only issue is that it passes the ingredients to your grocery list exactly as they are in the recipe. This is an issue, because the list of ingredients in a recipe are often for exact amounts for that specific recipe. Which makes perfect sense for a recipe, but looks weird and distracting when you're trying to find the item in the shelf. 

For example, here's a made-up list of recipe ingredients:

> - 1 clove of garlic, finely chopped
> - 1 1/2 lbs of chicken breast, sliced
> - 2 tablespoons of paprika

When I'm at the grocery store, I want to see as simple a list as possible, in the minimum increments I'm able to purchase. So I'd ideally want to see:

> - Garlic
> - 2 chicken breasts
> - Paprika

## Enter ChatGPT + Shortcuts

Turning loose data like ingredients into structured data like the simplified grocery list is such a perfect task for an LLM like ChatGPT, because you can just tell it what you want to do in natural language, and it will usually figure it out and do what you want, without having to write complicated language parsing rules. 

ChatGPT on iOS integrates nicely with iOS Shortcuts. So I made a 'clean my grocery list' Shortcut that:

1. Gets the list of reminders from my Grocery list in the Reminders app
2. Adds each reminder into a single variable and deletes from Reminders
3. Sends the variable of items to ChatGPT, asking it to turn it into a simple grocery list, only giving me the list, and making sure each item is on its own line
4. Takes the response, breaks it into separate items, and adds each item back to Reminders.

The only complicated part was playing around with the prompt until it looked right.

Could I live with the list of ingredients? Sure. And it's not worth re-writing them by hand to make them look nicer. But now I have a single button I can press on my phone to make my list nicer and easier to read!

I'll share the Shortcut in case anyone wants to try their own version. 

[Clean up Grocery List Shortcut](https://www.icloud.com/shortcuts/57f29c1ad22b4f339f18594867a0374c)
