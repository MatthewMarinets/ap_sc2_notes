# Adding items
To add an AP item requires 3 main steps:
* Add the actual effect to the mod: the unit, upgrade, ability, passive effect, etc
* Add the unlock trigger to the mod
* Add the item data to the client

Item data generally goes in ArchipelagoPlayer.SC2Mod, most often with an upgrade as an entrypoint.
Unlock triggers go in ArchipelagoTriggers.SC2Mod.
The required item data in the client is:
* the item name in item_names.py
* the item description in item_descriptions.py
* the item ID and parentage data in item_tables.py

In some circumstances, additional code may need to be changed in the client:
* Items may be added to item groups in item_groups.py
* Items may be added to logic rules in rules.py or locations.py
* Changes to items that are already released may require compat code in client.py

## Adding to the mod
### General
This is largely general sc2 modding knowledge, which I will not cover in detail here.
I recommend newcomers familiarize themselves with some of the data in ArchipelagoPlayer.SC2Mod, with good starting data types to understand being:
* UpgradeData.xml
* UnitData.xml
* EffectData.xml
* BehaviorData.xml
* AbilData.xml
* ButtonData.xml
* GameStrings.txt
* RequirementData.xml
* RequirementNodeData.xml

Most basic items can be implemented by just understanding these files. Graphical changes require getting into ActorData.xml, ModelData.xml, and SoundData.xml.

### Code Quality and Styling
Most (though not all) Archipelago devs do most of their data editing straight in the XML. This means we spend a lot of time looking at data IDs and prefer they stick to a style:
* Data entries added by Archipelago should begin with an `AP_` prefix
* Changes to non-AP data (such as enemy tags or AI flags or bugfixes) should include a comment with the word "override" present
* As much as possible, for items affecting one unit or a small class of units, try to include a passive icon in the command-card explaining what the upgrade does
  * If the unit is out of command-card space, we often use permanent Behaviors as extra icons in the behaviors section of the UI

Less strictly adhered to, though preferable:
* For an upgrade ID, if it only affects one unit, prefer including the unit's name near the start. Such as `AP_InstigatorBlinkOverdrive`
* For RequirementNode IDs, prefer cleaning them up a little to avoid internal `AP_` infixes. So prefer `AP_CountBioMechanicalStockpilingCompleteOnly` over `AP_CountUpgradeAP_BioMechanicalStockpilingCompleteOnly`
  * Also prefer simplifying IDs for long compound expressions and stripping serial number IDs tagged on by the editor
  * Note that making modifications in the editor may result in getting many unused requirement nodes that should be cleaned up, and these `AP_` infixes that are preferably removed
* If modifying in a text editor, prefer keeping entries in GameHotkeys.txt and GameStrings.txt alphabetical. The editor saves these files in alphabetical order, so leaving things unsorted can cause someone else to get a large cluttered diff.

### git etiquette
Saving in the editor will potentially create a bunch of spurious changes that clutter up a commit/PR in github and can potentially cause merge conflicts if multiple people try to merge such changes at the same time.
Use `git restore <filename>` to undo all local changes to a file since the last commit (include the `--staged` flag if you've already staged the file with `git add`).

Files to watch out for:
* `DocumentHeader` (recommend always discarding changes)
* Any file with `.version` extension (recommend always discarding changes)
* `PreloadAssetDB.txt`. This is a large file that the editor may make large changes to; pushing changes can be okay, but watch out for other PRs that may also be pushing to this file at the same time
* `GameHotkeys.txt` / `GameStrings.txt`. If the files have fallen out of alphabetical order, the editor will reorder them alphabetically. It's good to merge / make a PR with the fixed version, but prefer to add a PR comment highlighting the actual change you're making or be ready to resolve merge conflicts.

## Unlock triggers
Unlock triggers go in ArchipelagoTriggers.SC2Mod, with the effective code in `LibABFE498B.galaxy` and the GUI trigger logic in the file named `Triggers`.
Our unlock triggers are GUI triggers, so these are generally done in the editor.

### The unlock action
Most unlock actions will simply unlock a single upgrade, like:
```C
void libABFE498B_gf_AP_Triggers_Terran_unlockWraithResourceEfficiency (int lp_player) {
    // Automatic Variable Declarations
    // Implementation
    libNtve_gf_SetUpgradeLevelForPlayer(lp_player, "AP_ResourceEfficiencyWraith", 1);
}
```

Unlock triggers go in the `/TechTree/<race>/Unlocks/` folders.

**Note that unlock triggers must be robust to being run multiple times.** Every time the client sends a new unlock to the mod, it will send _all_ unlocks and the client will run all unlock functions.

### Registering the unlock action
To make sure the unlock trigger is actually called, add it to the CustomScript section of its category at the correct index. The category triggers are in `/BotCommands/Functions`, and might look something like this:
```C
    ap_triggers_processBitsInBitArray(
        lp_player,
        lp_bitArrayValue,
        libABFE498B_gf_AP_Triggers_Protoss_unlockAiurZealot, // 0
        libABFE498B_gf_AP_Triggers_Protoss_unlockStalkerShakuras, // 1
        libABFE498B_gf_AP_Triggers_Protoss_unlockHighTemplarAiur, // 2
        // ...
        libABFE498B_gf_AP_Triggers_Protoss_unlockVanguard, //27
        libABFE498B_gf_AP_Triggers_Protoss_unlockWrathwalker, //28
        libABFE498B_gf_AP_Triggers_Protoss_unlockReaver //29
    );
```

When registering a new unlock action, the category must match with the client-side `type` in the item_tables.py entry, and the argument index must match the `number` parameter in the item_tables.py entry. See [item_tables.py](#item_tablespy)

### Setting default tech
If the added item is a unit or an ability unlocked with a straight `TechTreeAbilityAllow` or `TechTreeUnitAllow` function, then it needs to be explicitly disabled by default. This is done by the `clear<race>Tech`, in the `TechTree/<race>/` trigger categories.

If default setup must be done, like giving a default upgrade, that is done by the `give<race>DefaultTech` triggers, also in `TechTree/<race>/` categories.

### git etiquette
Prefer to restore / not commit changes to `*.version` files, `DocumentHeader`, or `ComponentList.SC2Components`. The editor likes changes these files, many of which are binary files and thus don't have an easily-viewable diff, but they aren't actually necessary for anyone so the changes can be safely reverted.

Undo the changes on the command-line with `git restore **/DocumentHeader *.version **/ComponentList.SC2Components`

## Client-side changes
For most simple upgrades, this is generally only about 4 lines of code in the client repository.

### item_names.py
Add a variable to `item/item_names.py`, which controls the display name of the item in the Archipelago client and message boxes.
The variable name should be all-caps with words separated by underscores. The variable name should not start with an underscore.
Try to place the item name in a sensible place near other similar or related items; the file has many comments denoting such sections.

### item_descriptions.py
Add a description for the item in `item/item_descriptions.py`.
This will just be a dict entry mapping item name variable (set above) to a string containing the description.
The description appears in-client when the user hovers over the item name, and in the item repository external resource.
Note the in-client appearance handles box width by just adding newlines after periods, so try to keep sentences reasonably short.

There are some simple unit tests enforcing basic style guidelines on item descriptions, but they are not all-encompassing:
* All item descriptions should end in a period
* Avoid using double-spaces after a period.

It is the responsibility of the implementer and reviewer to try to spot typos and have reasonable grammar.

### item_tables.py
This defines the actual item data for interfacing between other components: the Archipelago server, the generation logic, and the unlock triggers.
The common arguments are:
* The item `code` / ID (client <--> server). This is an integer that should be unique among all sc2 item IDs.
  * Use the `SC2_<campaign>_OFFSET` constants to put items in separate ranges.
  * Be on the lookout for other PRs adding or affecting items for similar categories/races to yours -- there may be an item ID collision.
* The item `type` / category (client <--> mod). This is an enum entry that must match the category the unlock trigger is registered to. See [Registering the unlock action](#registering-the-unlock-action).
  * This category is also often used to automatically add the item to item groups in `item_groups.py`.
* The category `number` (client <--> mod). This is an integer from 0~29 that matches the argument index in the unlock register function. See [Registering the unlock action](#registering-the-unlock-action).
  * Note progressive items increase their `code`s in increments of 2.
* The item's `race` (item <--> generation logic). This is an enum entry saying what race the item belongs to. Multi-race items like filler or keys can go to the `SC2Race.ANY` enum entry.
* The item `classification` (item <--> generation logic & server) (optional). An enum representing the usefulness of the item, such as filler, useful, progression, trap.
  * Defaults to "useful".
  * Only progression items may be used in logic rules.
  * Units should generally be progression.
* The item's `quantity` (item <--> generation logic) (optional). Used to define how many copies of the item can appear in the item pool.
  * Defaults to 1
  * Note progressive items, with quantities like 2 or 3, should belong to a `Progressive` category, which use different unlock registration functions in the mod.
* The item's `parent` (item <--> generation logic) (optional). String representing a parent item name. Controls item culling logic during generation -- if a parent item is culled, the child items are also culled. For example, this is what removes Marine stimpack from the item pool if Marines are removed.
  * Defaults to no parent (i.e. never auto-cull).
  * Has a minor effect after generation -- if a player runs `/received` in the client, the parent parameter controls how the output is organized under headings.
  * More complicated culling rules, such as an item only being auto-culled if multiple parent items are all culled, are represented with logic defined in `item_parents.py`. When using such rules, the `parent` parameter may be set to a string from `parent_names.py`, which should match the culling rule associated with the desired rule in `item_parents.py`.

### item_groups.py
New items can optionally be added to explicitly-defined item groups in `item_groups.py`.
Many item groups are auto-generated from the item's race and type, so no action is required.
Some item groups that are more thematic, such as Protoss subfactions or Zerg infested, are hand-curated, so it is better to check on these item groups when adding a unit.

If a new item is very strong to the point of trivilizing worlds once it is acquired, it should be added to the overpowered items group.

## Testing
### Testing mod data
* Ziktofel has a test map with many pre-placed units, download pinned in the #sc2-dev channel. It is good for testing unit and ability interactions.
* After deploying mod files to the Starcraft 2 folder, it's possible to generate a new Archipelago game, use `/disable_mission_check` in the client to allow starting any mission, and start the mission.
  * Use editor commands like `makeunit <unit id>` to make units at the mouse cursor location, or `upgrade <upgrade id>` to give the player an upgrade.
  * Find a fast generate-and-start script in the yaml repository here: https://github.com/ap-sc2-documentation/yaml-repository/blob/main/devscripts/genstartsc2.py

There are a few ways to deploy mod files quickly. I recommend a script to just copy the .xml and .txt files from your repository clone into your Starcraft II/Mods/ folder. It's also possible to make a symlink from your Starcraft II/Mods/ folder to your repository clone, though this means doing a `/download_data` can write to your repository clone.

### Testing integration
It's important to test that the item_tables.py data matches what the mod expects.
This is destructive testing (can only be done once per world before requiring a new seed), so is best done separately from testing the mod data directly.

1. Deploy your mod files to the `Starcraft II/Mods/` folder
2. Generate a new world locally, start the server, and connect with a client
3. Start a mission where you can observe your new item being unlocked (building that can train your new unit, unit that can have your new upgrade, etc)
4. Verify your item is not unlocked yet
5. In the server console, run `/send <playername> <item name>` to send the item
6. Verify that the item is unlocked for the player in-game

I like to take screenshots of in-game descriptions and buttons to show them unlocking.
