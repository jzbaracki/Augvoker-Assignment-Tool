# Automating Buff Assignments for a Competitive Raid Team

A scheduling tool that turns combat-log data into a ready-to-paste assignment plan for a competitive World of Warcraft raid team, replacing a manual planning process.

**Skills:** algorithm design · constraint-based scheduling · API data processing · building tools for non-technical users · R (`tidyverse`)

## 

## The problem

In high-level raiding, a support role called the Augmentation Evoker boosts the damage of other players with a buff called *Prescience*. Getting the most out of it means:

* buffing whichever players will deal the most damage in each burst window of the fight,
* coordinating up to three Evokers so no two buff the same player at overlapping times, and
* redoing the plan whenever the roster or strategy changes.

Doing this by hand for every cast, across every Evoker and every fight, was slow and easy to get wrong. 



## How it works

1. **Data:** player damage in each burst window, calculated from Warcraft Logs combat data, plus a schedule of every planned buff cast (cast time, expiration, priority).
2. **Assignment:** a greedy algorithm fills casts in priority order. For each cast, it finds every existing assignment whose buff would overlap in time, removes those players from that window's damage ranking, and assigns the highest-ranked player left.
3. **Output:** the assignments are formatted as text for an in-game raid note (Method Raid Tools), so the raid leader can paste them in directly.

## 

## Results

The plan worked best when every Evoker cast on schedule. The main failure mode was timing: if an Evoker refreshed the buff outside its planned window, the assignments fell out of sync for the rest of the fight. Comparatively to other evokers, our top performing evokers were contributing an estimated 20-30% additional damage due to our assignment system.

## 

## Possible extensions

* Compare the greedy assignment against an optimal assignment solver.
* Update damage rankings during a fight instead of fixing them per window.

## 

## Repository contents

|File|What it does|
|-|-|
|[`analysis/prescience\_assignments.Rmd`](analysis/prescience_assignments.Rmd)|Data cleaning, the assignment algorithm, and the export|



