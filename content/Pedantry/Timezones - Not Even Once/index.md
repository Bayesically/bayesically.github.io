---
title: "Timezones - Not Even Once"
date: 2025-06-15
tags: [countries, timezones, pedantry]
draft: false 
---

# Whyyyy
## The nightmare begins
I remember watching a fantastic Computerphile video years ago now featuring Tom Scott explaining why timezones are [just the worst](https://www.youtube.com/watch?v=-5wpm-gesOY). That's not to say that they aren't super important and interesting, but there are so many caveats and edge cases that you will have a migraine by the time you're done working with them (and your code will probably be wrong).
*Yes, this includes the code I wrote to achieve this very post.*

## Why even have timezones?
Time is a construct. 

Why does it matter if the sun comes up at 4AM or 11PM? Couldn't we just have a single universal coordinated time?

***If this is your opinion, good luck to you. I think you're insane. All power to you, you anarchist, but we are not friends***.

For those who are still reading, I hope we can all agree that it makes sense if 12 noon is midday - by which I mean that the sun is at its highest point at 12 o'clock.

Sadly, the Universe has decided that the Earth will rotate at a jaunty angle, and as such your day will change length over the course of the year (except my Equatorians, you're chilling).

Back in the day, everyone just set their clocks so that noon where they were happened at 12:00. This is fine if you're only bothered about your exact city, but a nightmare if you want your train to arrive "on time" (*"it works on my watch!"*).

So there's a case for different areas having different times which aren't ideal for their exact location, but agree with the people nearby to you. The Brits get together and agree they should have the same time, but that there's no reason this should agree with dirty continental European time - perfect!

There are some complexities when your country's just absurdly large (looking at you, USA), so you draw some lines every 15° or so, give them all weird names (looking at you, Australian Central Western Standard Time [ACWST]) and call it a job well done. In China, it's always Beijing o’clock — even if you're closer to Kabul than the capital.

All these decisions and weird caveats result in some weirdness. Let's open the can of worms:

# What Time Is It Anyway?

*Before we get started - timezones make very little sense near the poles where day and night are just a suggestion. I've filtered out all the Antarctic research bases where the sun rises at 8PM.*

## Thicc with Two Seas (okay, Oceans)

South America can't even contain UTC-3. At the right time of year, Alejandro Selkirk Island and Trindade and Martim Vaz have the same time. They're also both islands hundreds of miles away from either edge of South America. 

![[utc-3_map.png]]
As Trindade doesn't observe daylights savings, they only share a time in the summer, but the width of this timezone of ~52.4° *should* be separated by a time difference of 3.5 hours. 

## A North/South Union

While the icy northern Cape Dyer on Baffin Island, Canada and the Pacific island of Rapa Nui (aka Easter Island 🗿) are kind of on opposite ends of the Americas. During the Northern Winter and Southern Summer, they both adopt UTC-5.
![[utc-5_map.png]]
These areas are pretty far apart. While that train might arrive "on time" it would also have to travel about 11,200km over a lot of water, a journey of about 16 days by boat ignoring the whole *getting beached on Illinois* issue.

## One Country, One Timezone
Let's face it, the big outlier was always going to be China!

(_Yes, I know the punchline has been “China” in both of these posts. I swear that’s coincidence, not geopolitics... [[Red Flags]]_)

China is about as large East-West as the USA. Every part of China officially uses UTC+8 (Beijing Time), all the way from Xinjiang in the West, to its border with Russia in the Northeast. That means that on the same day, noon can be as late as 3pm in the West while noon happens at 11am in the East.

Using that comparison with the USA (just the contiguous part), the USA splits this up into 4 timezones (Eastern/Central/Mountain/Pacific) which accounts for the 60°+ of spherical geometry. I'm sure anyone who's tried to watch national analogue television broadcasts in the USA is aware that doing the math(s) is a bit of a headache. I was once on holiday in the USA and missed the Simpsons because we crossed a state border. It's still a sore spot.

This means there's a complex and nuanced disagreement in Xinjiang regarding the usage of Beijing time and Xinjiang time (https://en.wikipedia.org/wiki/Xinjiang_Time) which I won't delve into as my sarcasm probably won't do the discussion justice.

To take a lighthearted approach - Were English southerners to move to Xinjiang where noon occurs at 3:15pm, and English northerners were to move to Eastern China (noon ~ 11:15am), the English would finally all be eating dinner at the same time?

![[utc_plus_8_zoomed.png]]
