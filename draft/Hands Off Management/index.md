---
title: "Hands-Off Management"
published: 2025-06-15
tags: [football, managers, data]
draft: false 
---

Every team needs one madman. That’s what the goalkeeper’s for.

They might be the ones screaming and yelling at their full backs with spittle running down their chin (Pickford, Kahn), just plain mental (Higuita), or the one five pints deep in his trackies on a Saturday afternoon (Király), but keepers do their job of stopping goals going in the net. But is there an ounce of footballing knowledge behind those skulls?

When the gloves come off, does the tactical nous shine through?

Let's start with a hypothesis - "The percentage of managers who played in a position should have no influence on whether that player becomes a top manager".

To summarise this slightly differently - "The percentage of players who are goalkeepers should match the percentage of managers who were goalkeepers". This highlights a slightly parallel assumption which we can test - "There aren't many non-playing football managers".

## Players by Position

There's certainly an *expected* answer to the question "how many players are there in each position?". There should be one goalkeeper, and then a 4-4-2 of defenders, midfielders, and strikers. (#)

That would put the estimated percentages of players in each position as something like:

| Position | (Theoretical) Percentage |
| -------- | ------------------------ |
| Goal     | 9.09%                    |
| Defence  | 36.36%                   |
| Midfield | 36.36%                   |
| Attack   | 18.18%                   |
But that's just theory, let's put some data behind this. If we go to Wikidata and put together a query like the following:

```
SELECT DISTINCT ?player ?playerLabel ?positionLabel ?clubLabel ?leagueLabel ?start WHERE {
  VALUES ?league {
    wd:Q9448     # Premier League
    wd:Q324867   # La Liga
    wd:Q15804    # Serie A
    wd:Q82595    # Bundesliga
    wd:Q13394    # Ligue 1
  }

  ?club wdt:P118 ?league.
  ?club wdt:P31 wd:Q476028.

  ?player p:P54 ?statement.
  ?statement ps:P54 ?club.
  ?statement pq:P580 ?start.
  FILTER(YEAR(?start) >= 2022)

  OPTIONAL { ?player wdt:P413 ?position. }

  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```
We'll get a list of players, their clubs (filtered to some obvious leagues) and make sure they're only recent signings (">=2022").

This returns a lot of players with positions that aren't quite as nice as "defender", so we can just make a quick list and "look up" those positions using the table below:

| Goal       | Defence          | Midfield             | Attack  |
| ---------- | ---------------- | -------------------- | ------- |
| Goalkeeper | Defender         | Midfielder           | Striker |
|            | Centre Back      | Central Midfielder   | Forward |
|            | Left Back        | Attacking Midfielder |         |
|            | Right Back       | Defensive Midfielder |         |
|            | Fullback         | Winger               |         |
|            | Central Defender |                      |         |
|            | Sweeper          |                      |         |
After doing that, we find something slightly different:

| Position | (Theoretical) Percentage | Actual Percentage |
| -------- | ------------------------ | ----------------- |
| Goal     | 9.09%                    | 12.6%             |
| Defence  | 36.36%                   | 29.7%             |
| Midfield | 36.36%                   | 32.3%             |
| Attack   | 18.18%                   | 25.4%             |
So *in reality* there are more attackers than a 4-4-2 might predict (*Claudio Ranieri looks on disdainfully*). There are probably reasons for this which are interesting but entirely unrelated to our question, so let's get back on track and do the same for managers. 

## Managers by Position

Let's pull the data:

```
SELECT DISTINCT ?club ?clubLabel ?leagueLabel ?manager ?managerLabel
                ?isPlayer ?positionLabel ?endOfPlayingCareer WHERE {

  VALUES ?league {
    wd:Q9448     # Premier League
    wd:Q324867   # La Liga
    wd:Q15804    # Serie A
    wd:Q82595    # Bundesliga
    wd:Q13394    # Ligue 1
  }

  ?club wdt:P118 ?league.
  ?club wdt:P31 wd:Q476028.  # Must be an association football club

  ?club p:P286 ?coachStatement.
  ?coachStatement ps:P286 ?manager.
  FILTER NOT EXISTS { ?coachStatement pq:P582 ?end. }

  OPTIONAL {
    ?manager wdt:P106 ?occupation.
    ?occupation wdt:P279* wd:Q937857.  # subclass of football player
    BIND("yes" AS ?isPlayer)
  }

  OPTIONAL {
    ?manager wdt:P413 ?position.
  }

  OPTIONAL {
    ?manager p:P106 ?playerStatement.
    ?playerStatement ps:P106 ?occupation2.
    ?occupation2 wdt:P279* wd:Q937857.
    ?playerStatement pq:P582 ?endOfPlayingCareer.
  }

  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
ORDER BY ?leagueLabel ?clubLabel
```

This query is a little bit more complicated. We got the managers and their teams, but we also then looked firstly ***if*** they played football professionally, and if so in what position.

You'll also see lots of faffing about fixing some data quirks in there. Some clubs will have head coaches instead of managers, often they're the same thing, sometimes a club won't be a football club (don't get me started) and even with all this work I still had to hand remove some clubs which Wikidata claimed were in the premier league but definitely are not. Looking at you, *C.D. Marathón*... Someone's been making some cheeky edits.

Firstly - there's are only one or two blokes who never played football professionally who appear in that list. Rangnick and Nagelsmann both manage national teams now, so they're no headache for our statistics!

## Head-to-Head

Now it's time, let's analyse the distribution of managers by position, using the same look-up table we made above:

| Position | Managers (%) | Players (%) |
| -------- | ------------ | ----------- |
| Goal     | 2.9%         | 12.6%       |
| Defence  | 32.4%        | 29.7%       |
| Midfield | 49.6%        | 32.3%       |
| Attack   | 15.1%        | 25.4%       |
By eye - there are clearly far fewer goalies who become managers, and far more midfielders who turn their hand to coaching. But obviously this is a great place to run some statistics.

Let's pull out our Chi-squared test (χ²) and we find that we can confidently say that:
- ***Significantly more*** midfielders become managers than would by pure chance (p<0.01)
- ***Significantly fewer*** goalkeepers become managers than would by pure chance (p<0.01)
- ***Marginally fewer*** attackers become managers than would by pure chance (p=0.05)

## 0-3-6-2
Putting these percentages into a managerial formation, the 0-3-6-2 doesn't look like a particularly natural tactic.

![[0-3-6-2.png]]
Long story short, once the gloves come off, the keepers are heading for the pundits' chairs, not the gaffer's office.