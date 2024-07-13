# Feature ideas
## Utility
* Checkpoints in no-builds that replenish the player's army
  * Back in the Saddle
  * Supreme
  * Conviction
  * The Infinite Cycle
  * Templar's Return
* Allow changing player colour during missions
* Scouting
  * Completing a mission can hint remaining checks or remaining challenge checks
* Deathlink
  * Instant mission fail? (Unfun)
  * Snipe / reduce to red main Command Center
  * Snipe / half-health lowest- or highest- health unit
  * **Note**: Relating deathlink to in-game units rather than mission failure also opens the possibility of _sending_ multiple deaths / mission

## New Items
* Workers for other races
* Filler +max supply (over 200)
* New mercs
  * ?Predator
  * New BCs -- theme after infantry / mech
* Merc cooldown reduction
  * Progressive 3x "-30s or -12.5% cooldown / merc tier" (--sraw)
* Mercs for zerg / protoss
* Relocate ebay / merc compound / armory
  * Make them float, like BW (--Alice Voltaire)
  * Make them teleport / jump, like Marauders campaign (--Phanerus)
* Hero units trainable from Merc Compound
  * Raynor, Tychus, Swann, Stetmann, Nova, Tosh, Odin
  * Hero abilities as more checks
* Hero randomization on no-builds

## Predators
From Envy Dragon, 2024-01-19
concept 1:
* by default, predators have 50 energy and 0 energy regen.
* by default, predators gain a "pursuit mode" toggle that drains energy at a constant rate, but grants increased move speed and armor(?)
* by default, retribution fields restore 1-2 energy for each target they deal damage to
* by default, predators rapidly regenerate energy after 5 seconds out of combat (or something)
* Cloak upgrade is replaced with "predators are cloaked in pursuit mode"
* New upgrade: "predators ignore unit collision in pursuit mode" or something
* New upgrade: "during pursuit mode, destroyed predators respawn at your main town hall" with a large cooldown
* New upgrade: "+25 max energy; pursuit mode now costs 25 energy to activate, but grants a 100hp shield on activation"

concept 2:
* replace charge with a point-and-click leap attack, damaging and slowing on arrival
* new upgrade: dealing damage to an enemy grants a temporary buff with a cooldown (damage or defense or both)
* new upgrade: retribution field gets bigger with consecutive attacks
* new upgrade: if target of attack has energy, each attack drains 20 energy to deal 20 extra to them? idk

concept 3:
* default: toggleable autocast, grants a teleport-dash (roughly charge range) that can only dash onto targets with an energy bar, then grants itself a 50 damage shield(?)
* new upgrade: dash also grants an attack speed buff
* new upgrade: dash has a feedback effect? idk
* new upgrade: killing an enemy deals X damage to units around that enemy (increased if target was Psionic)

Phanerus: a knockback effect like Artanis's resurgence (scale: melee reaper grenade) to help them retreat / clump enemies?

### Ability ideas
* [Baseline] Resource efficiency
* Knockback away from the predator
* cooldown-based Phasing Cloak that allows passing through surrounds to escape
* Centurion charge / leap
* [Passive] Retribution field size
* Melee EMP centered on the Predator
* [baseline?] +1 armour or bonus armour while moving

## Item Adjustment
* Evolved Carapace (Brood Lord) should also affect Guardians

### Multi-race
* Magnemania locally added probes to be built from CC
  * Workers may come from Merc compound (--Phanerus)
    * low command-card space (--Ziktofel)
* Could make probe a findable item
* Race swap can come later, but general idea is to leave preplaced units unchanged and only change workers / buildings

## yaml / options changes
* Be able to ban certain kinds of filler (no +minerals, no +gas, etc)
* Item groups
  * More detailed (mercenary, unit, upgrade, etc)
  * By difficulty
* Default difficulty set to normal instead of casual

## Modify missions
* [In_Utter_Darkness] Add a button to spawn a wave of enemies
* [The_Outlaws,Zero_Hour,NCO] Add a starting Merc Compound
* [Liberation_Day] Randomize units in the drop (Reaper, Marine, Marauder, Spectre, Ghost, Firebat)
* [All-in] Randomize artifact effect (artifact blast, Odin calldown, laser drill)
* [No-build] Buildable crack-team in no-builds (--Alice Voltaire)
* [No-build] Randomize heroes / units somehow

## Extra locations
* [Secret] Zero Hour: Tauren Marine
* [Secret] Piercing the Shroud: Murloc Marine
* [Secret] The Devil's Playground: Diablo, Lord of Terror
* [Secret] Haven's Fall: Gas Island
* [Challenge] Evacuation: Left Zerg Base
* [Challenge] Evacuation: Right Zerg Base
* [Challenge] Smash and Grab: Zerg Base
* [Challenge] The Dig: All Protoss Bases
* [Challenge] Supernova: Leftmost Nexus
* [Challenge] The Devil's Playground: All Zerg Bases
* [Challenge] The Great Train Robbery: Planetary Fortress
* [Challenge] Echoes of the Future: Clear all bases
* [Challenge] In Utter Darkness: Omegalisk (1 of 3 or all 3?)
* Maybe look towards achievements

### Maybe use speedrun achievements
Proposed by Berserker on 2023-10-01. Looking towards vanilla speedrunning achievements
| Achievement          | Mission              | Time         | Difficulty |
| -------------------- | -------------------- | ------------ | ---------- |
| Be Quick or Be Dead  | The Outlaws          | 10:00        | Hard       |
| 28 Minutes Later     | Outbreak             | 5th night    | Normal     |
| Jailhouse Rock       | Breakout             | 25:00        | Hard       |
| Blitzkrieg           | Media Blitz          | 20:00        | Hard       |
| Hit & Run            | Smash and Grab       | 15:00        | Hard       |
| Hard Core            | The Moebius Factor   | 6 structures | Hard       |
| Maar-ked for Death   | A Sinister Turn      | 25:00        | Hard       |
| Overmind Dead Body   | Echoes of the Future | 20:00        | Hard       |
| Speed Too!           | Shatter the Sky      | 25:00        | Hard       |

## New Mission orders
* Funnel -- A triangle where you start with a full row, beat a mission to unlock missions below it, rows get narrower until width 1 is the goal
* Hourglass -- like funnel, but re-widens after a pinch point. Beat the middle bottom mission to win
* Plaid -- grid with every 4th mission removed
* Ring -- like grid with middle removed (--Salzkorn)

### Theory
Mission orders are ultimately characterized by just a few parameters:
* Connectivity, ie average number of missions unlocked by beating a mission
* Optionality, ie how many missions are unavoidable vs you have choices and can never do one
* Length, ie how many missions do you actually need to beat
* Size, ie how many missions are there
* Change, ie how do the above characteristics change as more missions are beaten
* Presentation, ie how intuitive is progression

* Optionality / length / size can probably be simplified to just 2 parameters

## Generalize mission orders
* Current:
  * vanilla
  * vanilla shuffled
  * mini campaign
  * grid
  * mini grid
  * blitz
  * gauntlet
  * mini gauntlet
  * tiny grid
* Consolidate into categories
  * Vanilla: react to mission exclusions
  * Vanilla shuffle: react to mission exclusions (vanilla shuffle, mini campaign)
  * Grid: n x m grid; beat a mission to unlock adjacents (grid, mini grid, tiny grid, 4x6, 5x6)
  * Staircase: n rungs of width m. Beat a mission to unlock the next rung (blitz)
  * Linear: linear set of missions (gauntlet, mini gauntlet)

### Minor
> if you do end up fiddling away with that yourself, it might be best to also have another or to have a mission make itself available on grid if its own goal is completed; there's currently an unintuitive behavior if a mission completion gets collected in an area of the grid you haven't reached yet, the surrounding missions become available but the collected mission doesn't 
> -- Magnemania, 2023-10-04

### Discussion 2024-01-24
> as a fan of the vanilla shuffled setting it's a shame the HotS and LotV are so much more linear than WoL, I would love a shuffle setting that keeps the general structure but loosens the structure a bit like making it so you only have to do Kaldir or Char instead of both and same with Korhal/Shakuras and stuff like that  
> ...  
> I think the WoL campaign shuffle is a really good middleground
> 
> --Genderdruid

> I do not like having massive grids, I like having some amount of direction I need to go  
> grids are too open  
> ...  
> what I really want out of mission orders is two things:  
> 1. I want a generic "campaign" mission order that is dynamic and grows and shrinks depending on how many missions you have
> 2. I want the ability to have up to three (or more?) non-vanilla mission orders in one game, like three Gauntlets, three Grids, etc.  That way I can have one for each race all in one slot without being forced to do the big big ones like Vanilla Shuffled
> * * This will matter more once more campaigns start getting added, but I'd also like to be able to divide the mission orders up by race so I can include a bunch of missions across multiple campaigns, and the game collects them and gives me randomized Terran, Zerg, and Protoss campaigns out of them
> 3. I want the ability to adjust the amount of missions each race has in a given mission order.  That way I can "normalize" them within a grid so that they have equal presence, but also have it adjustable to allow for any funky mission order ideas people come up with
> * * (note: if this is too difficult to implement, a simple "normalize" feature would be equally appreciated by me)
> 
> --Alice Voltaire

* Can use existing "Shuffle Campaigns" option to factor into Multi-X mission orders
* Should probably adjust shuffle campaigns to restrict by campaign, faction, or none
  * Maybe give special treatment to prologue / prophecy / epilogue?

### Feedback
> Hey there, been playing a lot of Archipelago lately, and I've encountered a couple issues with my runs, that kind of ruins the fun for me.
> 
> First, it's when I mix all campaigns to play some small scale grid or equivalent (I don't enjoy full campaigns nearly as much), and the units/upgrades distribution seems really skewed towards a single race each and every time (to a ratio of like 80%-90% of all unlocks being for one of the three races, making playing the other 2 just not great).
> 
> Second, the logic really railroads the whole randomizer from what I could test, giving always the same few units to start with, and as someone who enjoy both randomness and difficulty, I tend to just switch the logic off, but that comes with it's own load of issues. The worst one being that it forces Grant Story Tech on, making all no build missions, well, the exact same as Vanilla (and uh, I tend to play mods and stuff like this to get away from replaying Vanilla for the 20th time).
> 
> I also have a feeling the distribution of locations throughout the 4 options you get is not balanced. more than half of them are in the "Extra" category (about 300), when only about 15 are in the "Challenge" one. (And let's not talk about things like Killing the Protoss on Welcome to the Jungle is a challenge, but Killing the Protoss on The Dig doesn't even exist, when it's the exact same thing).
> 
> Lastly, but that's really more of a personal preference, but some units are just stupid. Cost reduction on Ghosts for example, cutting it by more than half, when it's already a top tier unit. Or Siege Tanks having 3 different upgrades for Range when Sieged ? Not sure they need all that, or at the very least it could be combined into one.
> 
> Anyway, I don't want this to be purely negative. I've been playing this a lot because I enjoy it, but I want to be able to replay a randomizer with a fresh run, not having the same issues and OP stuff soloing campaigns every time. Keep up the good work. And thanks for the mod.

[--Stormzarn 2024-06-15](https://discord.com/channels/731205301247803413/980554570075873300/1251641950499508405)

> My feedback here is that upgrades really need proper rebalancing, and to please stop using "We copy SC1 numbers" as a balancing point, because it's lead to really unfun designs and balance for me. Strong upgrades can be exciting when they're really rare, but a lot of the upgrades tend to "this unit is so much stronger now that you can solo spam it in 80% of missions to get through them", and that's not even when they have all of their upgrades
> 
> And yes, I could go to vanilla upgrades only, but just playing vanilla WoL randomizer I've done plenty, LotV has little of interest with vanilla only, and HotS has this problem even worse because you combine evolutions 
> 
> I really like it when you have to scrap your way through stuff, or have to check locations and back out to get enough to finish something somewhere else, and that just doesn't happen outside of multigames where you get very few of your own checks for me at this point, and I'm not having fun
> 
> Please don't disregard my feedback with "You can create your own yaml to fix it", that does not acknowledge or fix the issue
> 
> I have created my own yaml to fix this, and it is a lot of work and honestly? I usually want to play mods like this to get away from designing stuff

[--Mindhawk, 2024-06-15](https://discord.com/channels/731205301247803413/980554570075873300/1251645452118396989)

## Tracker
* Indicate locked items
* Indicate excluded items
* Show hinted items
* Show who sent acquired items
* Show time when item was acquired
* Cooler backgrounds / css?

## Trap items
* Fun to think about, but must be fun to play with
* HotS had transmission traps
* Hard to balance with logic, as logic must still apply with traps collected
  * Note: If units receive baseline buffs without updating logic, a trap can remove the buff without breaking logic
* Two categories of traps: transient and persistent

### Persistent
* Negative filler (--Sraw)
  * -starting money / supply
  * -max supply
* Own unit abilities must be researched in-mission
  * Stim
  * Liberator defender mode must be researched
  * Siege mode must be researched (would break Dig opening)
    * Sraw: Make mercs always have abilities unlocked without researching, replace critical units in no-builds with merc counterparts
* Re-apply nerfs
  * Tech reactor cost + build time back to vanilla
  * Auto-refinery cost + build time
  * Kerrigan leaping strike causes auto-attack range reduction
* Own unit nerfs
  * Yamato damage reduced to 240 (void ray health - 10, patch 4.7.1)
  * Bootleg cloak -- cloak can't be turned off until energy is exhausted (see Grant talking WoL reversed Cutthroat)
  * Unsieging now costs money
  * Maw DTs get activateable cloak instead of permacloack
* Remove baseline items (*evil*)
  * SCVs
  * Tech Labs

### Transient
* *Pull the Boys*: Your workers are teleported to your army
* **Note** it's lot of extra work to get mission-specific details for each map
  * Most of these are also probably intended as jokes
* Set player color to rainbow, must be reset with `/color`
* Swap numbered hotkeys around
* Un-updagrade a building (automated refinery -> regular refinery; tech reactor -> reactor)
* "Snipe" / reduce a building to red
* Spawn a torrasque
* Spawn a small attack
* *evil* Mission-killers
  * **Note** maybe these could be caused by deathlink?
  * Spawn the Odin
  * Spawn a leviathan
  * Spawn a mothership
  * Enemy gets a laser drill
