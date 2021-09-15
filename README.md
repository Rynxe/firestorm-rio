# Firestorm RIO

A raider.io like M+ scoring system for Firestorm Servers.
https://keepdying.github.io/firestorm-rio/

## Frequently Asked Questions

### How does this work?

All data is **parsed** from Firestorm's website (https://firestorm-servers.com/en/challenge/index) by using Selenium.

### How do you score runs?

Exact scoring formula is given below:

```
    dungTimers = [+1 Timer, +2 Timer, +3 Timer]
    keylvltoscore = [...] # taken from raider.io addon
    
    max_time = dungTimers[0] + 600  # assume max deplete time 10 min
    deplete_score = keylvltoscore[dungLevel - 2] + 0.01 # If depleted score goes down to -2
    timed_score = keylvltoscore[dungLevel]
    up_score = keylvltoscore[dungLevel + 1] # when timed +2 or +3, score goes up to +1 
    
    if timer >= max_time: # if went pepegas
        return deplete_score
        
    elif max_time > timer > dungTimers[0]: # if depleted
        return (((timer - max_time) / (max_time - dungTimers[0])) * (deplete_score - timed_score)) + deplete_score
        
    else: # if timed
        return ((timer / dungTimers[0]) * (timed_score - up_score)) + up_score
```
This should give similar scores like in raider.io BfA Season 4.

### Some of my runs is missing?

If your run doesn't appear on Firestorm website, I can't parse that. Also If your run didn't get parsed before weekly reset, You won't be able to see it.

Keep in mind current data is gathered over 2-3 weeks by parsing manually so If you don't see your run 3 months ago don't blame me. 

### When data is gonna be parsed again?

It is set to update in every 15 mins. But Github Actions can be delayed because of high load. You can check actions for latest updates.

### How can I contact you?

Discord: keepdying#5821