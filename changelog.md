# Changelog
# API 4 / 2025 release / Archipelago version 0.6.4
These notes may be somewhat incomplete.

## General
* Raceswaps -- all build missions in WoL, HotS, LotV, prologue, and prophecy now have alternate versions to play as other races
  * May require non-vanilla items to beat or may start with non-vanilla units
* New mission orders:
  * Hopscotch, which alternates between 1 required mission and pick-1-of-2 missions
  * Golden path, a dynamically-sized WoL-like order with a main questline, sidequests, and mission count thresholds
  * Custom, a fully-customizable mission order. See the custom_mission_order doc for details
* Old mission orders Blitz and Gauntlet have been reworked to be dynamically-sized
* Mission keys -- require a special "key" item to unlock a mission
  * Useful for tying progression to a multiworld without shooting ahead
  * Useful for diluting power-increasing items in the item pool
* Victory cache -- configure how many items you get for completing a mission
  * Useful for coordinating location counts and rates with other games in multiworlds
* New logic level `any_units`. Behaves similar to `no_logic`, but guarantees units appear earlier
* Void Trade -- trade in-game units with other sc2 players in the multiworld
* Morphling -- a zerg unit that can't attack, but allows you to morph advanced strains without having the basic unit (opt-in)
* In-game objectives now display check counts which are responsive to restarting missions after partial completion
* The sc2 client now supports launching from the links on a room page

## Client
* Extraneous logging tabs have been removed
* Hovering over an item in the client will now display the item's description in a tooltip
* `/received` can now show most-recently acquired items with `/received recent`

## Options
* Options have been sorted into option groups on the webhost
* `start_inventory`, `locked_items`, `excluded_items` now all accept amounts of items to start/lock/exclude,
  and support item groups
* New option `unexcluded_items`, which allows marking an item as no longer excluded, but not locked
  * Useful for keeping items that were excluded as part of an item group
* New location inclusion options -- `basebust_locations`, `speedrun_locations`, `preventative_locations`
  * These location categories are flag-based; that is, a speedrun location will be a mastery or challenge
    location as well
* Location inclusion options now accept a new value -- `half_chance`, to give each individual location of
  that category a 50% chance of being included
* `exclude_overpowered_items` -- control whether to automatically exclude a curated list of items deemed
  overpowered in a boring or over-centralizing way (promoting repetitive play), such as Ghost Brood War cost,
  mind control, or Battlecruiser ATX Lasers
  * This may also be tuned by excluding the Overpowered Items group, and unexcluding items the player may
    want to keep
* `difficulty_curve` -- Easier missions are now less likely to appear later in a campaign;
  set this to `uneven` for the old behaviour
* `filler_items_distribution` -- controls the relative likelihood of different filler items appearing
* `filler_percentage` -- mandates a minimum percentage of the item pool that will be filler items
* `mission_order_scouting` -- Get a preview for the item category (filler, useful, progression) of accessible locations
* Nova, Kerrigan, and Spear of Adun now have options to limit the amount of abilities/weapons/passives that will generate
* `selected_races` -- Decide which races' missions will generate; useful now that raceswaps mean campaigns aren't tied to races
* `war_council_nerfs` -- Reduces the baseline power level of protoss units and adds items to recover
  LotV power levels. See [items](#new-items)
* `enable_race_swap` -- Allow alternate versions of missions where you play as a different race to appear in the pool
* `key_mode` -- Select arrangements of key items required to unlock missions
* `mission_race_balancing` -- control how strongly the mission generator will balance selection of missions
  belonging to each race
* `enable_morphling` -- Enable a non-combat Morphling unit for zerg that allows building any morph unit
  without unlocking the base unit
* `mercenary_highlanders` -- Optionally disable a new behaviour where mercenary Ultralisks and
  Battlecruisers are limited to only having one at a time even with unlimited merc cooldowns unlocked
* `victory_cache` -- Control how many bonus checks are awarded for completing a mission
* `player_color_nova` has been added after being missing last release
* `enabled_campaigns` replaces the old `enable_*_missions` for various campaigns to instead represent them as
  one consolidated list
* `vanilla_items_only` replaces the old `enable_*_items` for "bw", "ext", and "nco" categories
  * People didn't know what each group meant and new item group selection meant
    it wasn't worth maintaining some of these broad classifications
* `two_start_positions` replaces the old `grid_two_start_positions`, as it now applies to hopscotch and golden path
* Options referring to `spear_of_adun_autonomously_cast` have been renamed to `spear_of_adun_passive`
* `required_tactics` now takes a new logic level option `any_units`
* New options to limit the maximum number of items of a group:
  * `kerrigan_max_active_abilities`
  * `kerrigan_max_passive_abilities`
  * `nova_max_weapons`
  * `nova_max_gadgets`
  * `spear_of_adun_max_active_abilities`
  * `spear_of_adun_max_passive_abilities`
* `nova_ghost_of_a_chance_variant` allows playing NCO-style Nova in the WoL mission Ghost of a Chance
* `grant_story_tech` reworked from true/false to three options: `grant`, `no_grant`, and `allow_substitutes`
  * `grant` and `no_grant` function like the old true and false options
  * `allow_substitutes` functions like `no_grant`, but allows some macro-mission items to get Kerrigan
    through the start of Supreme without needing specific Kerrigan abilities
* New options for controlling Void Trade:
  * `enable_void_trade`
  * `void_trade_age_limit`
  * `void_trade_workers`
* New options for tuning the new filler items:
  * `maximum_supply_per_item`
  * `maximum_supply_reduction_per_item`
  * `research_cost_reduction_per_item`
  * `lowest_maximum_supply` -- controls the lowest your maximum supply cap can go no matter how many
    Reduced Maximum Supply items you acquire
* New colour options are added, usable with any `player_color_*` option

## Host settings
* Can now set the game to start in windowed mode with host option `game_windowed_mode` or by running `/windowed_mode` in the client
* The following yaml options can be overridden by the user in the sc2 options of the host.yaml file:
  * `game_difficulty`
  * `game_speed`
  * `skip_cutscenes`
  * `disable_forced_camera`
* Window startup and launcher display aesthetic details can be controlled with the following sc2 host.yaml options:
  * `terran_button_color`
  * `protoss_button_color`
  * `zerg_button_color`
  * `window_width`
  * `window_height`
* `show_traps` -- controls whether item rating scouting displays traps as distinct from filler; default false

## New locations
* Added many new Mastery locations:
  * The Dig enemy bases (Mastery)
  * Evacuation enemy bases (Mastery)
  * Smash and Grab Kerrigan's base (Mastery)
  * Rendezvous speedrun reinforcements (Mastery)
  * Reckoning Odin before it moves out (Mastery)
  * Temple of Unification Bases (Mastery)
  * Dark Whispers Kerrigan's base (Mastery)
  * Rak'Shir in under 15 minutes (Mastery)
  * Salvation kill the brutalisk (Mastery)
  * Essence of Eternity win with fewer than 15 Kerrigan kills (Mastery)
  * Amon's Fall clear all the volcanoes at once (Mastery)
  * Sudden Strike kill the Zerg base (Mastery)
* Several new challenge locations
  * Lab Rat in under 10 minutes (Challenge)
  * End Game destroy all the Orbital Commands (Challenge)
* Several new extra locations

## New items
* War Council -- all Protoss units can optionally start at their pre-war council state
  * For melee units, this means they are at the power level of the mission they are introduced in
  * For non-melee units, this means a custom nerf to bring their power level down close to their melee cousins
  * Recover their power level by finding an upgrade item
* New Units
  * Terran
    * Dominion Trooper
    * Devastator Turret
  * Zerg
    * Pygalisk
    * Infested Marine
    * Infested Bunker
    * Infested Diamondback
    * Infested Siege Tank
    * Bullfrog
    * Infested Banshee
    * Infested Liberator
    * Primal Igniter (Roach morph)
    * Tyrannozor (Ultralisk morph)
    * Overseer (now with creep tumors)
    * Devouring Ones (merc Zerglings)
    * Hunter Killers (merc Hydralisks)
    * Wise Old Torrasque (merc Ultralisk)
    * Hunterling (merc based on Dead of Night co-op mission)
    * Yggdrasil (merc Overlord)
    * Caustic Horrors (merc Roach)
    * Bile Launcher
    * Nydus Worm
    * Echidna Worm
  * Protoss
    * Stalwart (Purifier Immortal)
    * Skirmisher (Tal'darim Phoenix)
    * Intercessor (Aiur Void Ray)
    * Dawnbringer (Purifier Void Ray)
    * Mistwing (Nerazim Scout)
    * Caladrius (Purifier Scout)
    * Oppressor (Tal'darim Scout)
    * Skylord (Tal'darim Carrier)
    * Trireme (Purifier Carrier)
    * Elder Probes (one-time warp-in per mission)
* New upgrades:
  * Auto-turret (Warhound)
  * Reconstruction (Instigator)
  * Blink Overdrive (Instigator)
  * Aberration upgrades
  * Defiler upgrades
  * Corruptor upgrades
  * Sensor Tower upgrades
  * Archon upgrades
  * New merc upgrades for Terran
  * New merc upgrades for Zerg
  * Predator item rework
  * SCV Jump Jets
  * Science Vessel Tactical Jump
  * Medivac Resource Efficiency
  * Fusion Core reactor: extra energy regen near Fusion Cores
  * Hive Mind Emulator and Psi Disrupter upgrades to work vs Protoss/Terran
* New filler items:
  * Increased maximum supply (beyond 200 cap)
  * Reduced maximum supply (below 200, trap item)
    * Note this item doesn't generate by default; increase its weight in `filler_items_distribution` to get it
  * Faster shield regen
  * Faster building construction speed
  * Faster upgrade research speed
  * Lower upgrade research cost

## Balance Changes
* Reaver Resource Efficiency split into two items (100/100/2 -> 50/25/1)
* Ghost Resource Efficiency split into two items (125/75/1 -> 25/25/1)
* Spectre Resource Efficiency split into two items (125/75/1 -> 25/25/1)
* Scout Resource Efficiency split into two items (125/25/1 -> 75/25/0)
* Predator Fury removed
* Scout Photon Blasters no longer gives additional bonus vs light
* Rogue Forces (unlimited merc charges) split into Terran and Zerg versions
* Spore Crawler bonus vs biological removed from baseline and recovered by getting an item (Caustic Enzymes)
* Destroyer Reforged Bloodshard Core reworked to give a smaller bonus to bounce damage at all charge levels rather than one large bonus at max charge
* Oracle Stasis Calibration now only allows attacking stasised enemies for the first 5 seconds rather than the entire duration

