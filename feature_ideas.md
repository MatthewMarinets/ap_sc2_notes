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
