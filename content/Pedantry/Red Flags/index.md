---
title: "Red Flags"
published: 2025-06-15
tags: [flags, countries, pedantry]
draft: false 
---

# What's the Biggest Red Flag?

I've been fed an alarming number of short videos lately featuring comedians trying out some recycled material that goes something like: "I've been dating this girl, and she's got a big red flag... turns out she's [insert nationality]."

Cue awkward laughter and a national stereotype. Classic stuff.

Naturally, this raises a question far more interesting than the joke itself: **which national flag actually has the most red in it?** I don't care if comedy makes me laugh, but it must be accurate. Some say I'm a pedant...

## Methodology: In Which I Take This Too Seriously

I downloaded images of each country's national flag from a [github repository](https://github.com/hampusborgos/country-flags) and wrote some code to calculate the percentage of each flag that is red.
### Attempt 1: Naively RGB

Just count the red, innit? Count a pixel as red if its red channel (R) is greater than 150, and greater than both green and blue. This sort of works. Until it doesn't.

Kyrgyzstan and North Macedonia both came back as 100% red. Their flags are visibly half yellow. Turns out yellow is red + green, and naive RGB logic treats anything vaguely warm-toned as "red enough."

Looks like we need to up the complexity...

### Attempt 2: CIELAB and Accepting My Fate

So I did what any rational person would do: I switched to the CIELAB colour space and calculated ΔE (Delta E) 2000 values — which approximate human-perceived differences between colours — from pure red.

*(Shoutout to the International Commission on Illumination (CIE) for doing all the hard work here)*

According to the accepted wisdom:
- ΔE < 1 is imperceptible
- ΔE ≈ 5 is visible
- ΔE ≈ 20 is enough that you'd probably call it a different colour entirely

So I went with 20. Anything within that boundary gets counted as red. Want to see what that looks like? Here's a nice visual with a black line around the blob of "red enough".

![[./red.png]]
*(This isn't the whole gamut and there's some arbitrary L value chosen here, and a* and b* are coordinates I won't bother to define or explain, but look at the pretty colours!)*
## Results: Here Are Your Red Flags

Based on the percentage of non-transparent pixels falling within that ΔE < 20 range, here's your top 10:

- China (cn): 97.52%
    
- Morocco (ma): 96.84%
    
- Isle of Man (im): 94.14%
    
- Turkiye (tr): 93.93%
    
- Vietnam (vn): 93.26%
    
- Hong Kong (hk): 91.39%
    
- Kyrgyzstan (kg): 90.78%
    
- Tunisia (tn): 90.59%
    
- Albania (al): 86.96%
    
- Wallis and Futuna (wf): 84.99%


Yes, **China takes it**. So the joke works. But it's a crowded field. You could swap in Morocco or Vietnam and your joke still scans. I've probably just made some jokes more racist, but maybe more clever as well?

## Caveats

- **Caveat #1**: Lots of these countries might be more or less states recognised internationally. I let random peeps on github do the politics for me. Wallis and Futuna (#10) is definitely a part of France, the Isle of Man (#3) is a crown dependency. 

- **Caveat #2**: "Biggest" is technically wrong. I measured **percentage**, not area. Yes, you can print any flag at any size. No, I don’t want to have that debate. It’s dumb maths for a dumb joke.
	- If you *really* want to get into it, there's probably an argument to be made that one should consider different aspect ratios. ***If you care about this: Leave me alone, I don't respect your opinions.***

---

So next time someone makes a lazy red flag joke, you can one-up them with a fully sourced, CIELAB-validated answer. It’s China. 97.52%. (No that's not a tariff).

Top 9 with their red removed:

![[./compilation.png]]

To imagine the bottom 50 flags by redness, just close your eyes (all are 0% red). Nicaragua and El Salvador share the glory for the least detectable amount of red (bottom once remove zeroes).

Here's a CSV for the proper nerds: ![[./redness_scores.csv]]