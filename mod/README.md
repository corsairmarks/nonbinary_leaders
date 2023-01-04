# Overview

Would you like your leaders to have a chance to have gender identities that vary from the gender presentation of their portraits?  Do you want your leaders to be able to use "they" pronouns?  Then this mod is for you!

The effects are more noticeable for species portraits that have sexual dimorphism, but that is not a requirement.

# Changes

Stellaris supports 3 gender states in code (`male`, `female`, `indeterminable`), which correspond to the pronouns he, she, and they.  Whether a species uses binary male/female genders (the default) or consists solely of a single gender identity is configurable during empire creation in the Species Name tab.  This mod adds a chance for leaders adopt a new gender identity when they are spawned by the game (20% chance to change from their assigned gender identity - 10% for each of the other two genders).

With this mod, leaders of a binary-gendered species who become indeterminable have a 50/50 chance of presenting as feminine or masculine. Unfortunately due to underlying game changes, it is no longer possible to influence which portrait a leader uses via in-game flags. Although possible in the past, that means leaders will no longer be able to have portraits where their gender presentation is different than their gender identity. Females will always present as feminine, males will always present as masculine, and indeterminables will randomly present as either feminine or masculine.

This mod optionally adds copious log entries to game.log file when running; use the in-game console to enable it with `event nonbinary_leaders.3`.  Here's where you can find the game.log file: `%USERPROFILE%\Documents\Paradox Interactive\Stellaris\logs` (Windows), `~/Documents/Paradox Interactive/Stellaris/logs` (MacOS), or `~/.local/share/Paradox Interactive/Stellaris/logs` (*nix).  To turn tracing off again, use the same command again.

Lastly, you can log detailed information about all of your leaders (owned and pool) to game.log by firing my debugging event from the in-game console: `event nonbinary_leaders.1000`.  I used this to help understand the game state while developing and decided to leave it available for future use.

## Compatibility

This mod is implemented via an event attached to `on_leader_spawned` to add the % chance to reroll a leader's gender identity.  That part should be widely compatible with other mods, including my other mods that also affect leader spawning:

* [Special Leadership Privileges for Battle Thralls and Bio-Trophies](https://steamcommunity.com/sharedfiles/filedetails/?id=2496357447)
* [Leader Traits: All Eligible Species Traits](https://steamcommunity.com/sharedfiles/filedetails/?id=2499031295)
* [Leader Traits: Enhanced Randomisation](https://steamcommunity.com/sharedfiles/filedetails/?id=2553806265)
* [Leader Traits: Scientist AI Assistant Upgrader](https://steamcommunity.com/sharedfiles/filedetails/?id=2498166286)
* [Retain Leaders from Integrated Subjects](https://steamcommunity.com/sharedfiles/filedetails/?id=2553818684)

As discussed above, a compatibility patch is necessary to fully support varying gender presentation for other mods that add species portraits.  By default, this mod supports all the built-in, gendered species classes and any sexually dimorphic portraits in each of those classes.

If you would like me to implement a compatibility patch (to support feminine/masculine presentation from sexual dimorphism), please leave a comment asking nicely, what you want, and with a link to the mod you want to be compatible.

Built for Stellaris version 3.6 "Orion."  Not compatible with achievements.

### Known Conflicts

Any other mods that adjust the human portrait groups (not individual portraits), including my mod [Human Portraits: Unified](https://steamcommunity.com/sharedfiles/filedetails/?id=2820018928).

### When to Install

This mod can be added to or removed from your savegame safely without issue.  If you remove this mod, any leaders which already have had their gender identities set will remain as-is but new leaders will only spawn to match the gender usage of their species class.  Leader portraits will revert to the default selection criteria.  Although leaders retain any custom flags set on them, this doesn't affect gameplay.

## Known Issues

### Limitations

Only leaders that are spawned into the leader pool (whether the pool is for a player or an AI) will have a chance to randomize their gender identity.  Leaders created through other means (for example, the `create_leader` and `clone_leader` effects) are unaffected.  Generally those are special event leaders and are intended to have a particular gender.

Leaders which select to identify as nonbinary (`indeterminable`) will not show a gender in their tooltip.  This is as-designed by Paradox, because the original purpose of the third gender is for non-gendered species (i.e. has no concept of gender at all).  Showing the line "Gender: Indeterminable" for every one of their leaders would be redundant.

Finally, it is not possible to allow for selecting gender-nonbinary rulers during species creation.  The logic for the species customization screens is part of the core Stellaris game and is not alterable by modders.

## Changelog

* 1.0.0 Initial version
* 1.1.0 Maintenance release
	* More flags to help with understanding what randomization happened for a leader
	* Prepare code for submod
	* More legible font for thumbnail
* 1.2.0 Add `on_action` to flag mod as installed when loading a single-player game
* 2.0.0 Update for compatibility with Stellaris version "Lem"
	* Simplify leader re-creation code with new features from 3.1.1
	* Simplify leader re-creation code to use `clone_leader` instead, eliminating redundant checks
	* Origin: Clone Army species that are infertile will not randomize their gender presentation
	* Unfortunately, currently not able to offer an event to choose your starting ruler's pronouns without the portrait changing
* 2.1.0 Improve gender presentation swaps to also use cloned leaders - leaders who alter their gender presentation now reliably have the correct portrait
* 3.0.0 Update for Stellaris version 3.6 "Orion" (also including changes from versions 3.5 "Fornax," 3.4 "Cepheus," 3.3 "Libra," and 3.2 "Herbert")
	* Add support for legacy human portraits
	* Add support for aquatic portraits with sexual dimorphism
	* Add support for toxoid portraits with sexual dimorphism
	* Use new `species_gender` trigger to support the new mono-gender species option for all base game for all portraits with sexual dimorphism (Paradox only added support for Humans)
	* Substitute my nonbinary icon for the indeterminable one added in Stellaris version 3.2 "Herbert"

## Source Code

Hosted on [GitHub](https://github.com/corsairmarks/nonbinary_leaders)

### Development Notes

It is best to clone this repository into `<Stellaris User's Directory>/Paradox Interactive/Stellaris/mod`, and then make a connection to the `mod` folder via a `*.mod` file's `path` property.  That will ensure the game can see the files, and also that CWTools will parse them.  Also note that the README.md file exists in the `mod` directory but is symbolically linked in the root directory.

# Request for Collaboration

I'm looking for one or more people knowledgeable about modding portraits and models for Paradox games.  With my newly-discovered ability to unlink the in-game gender of a leader from their appearance, I want to create some additional options for the human portrait set.  Notably, I'd like to have more variability in gender presentation of the portraits.  The existing portraits only offer feminine and masculine presentation.

# Special Thanks

Thanks to Paradox Development Studios (a subsidiary of Paradox Interactive) for making [Stellaris](https://store.steampowered.com/app/281990/Stellaris/), a game that I have enjoyed playing and modifying.  This mod would not be possible without their efforts to add aliens which do not use a gender - a feature I repurposed for this mod!  They did all the heavy lifting to make their localisation (translations) work with 3 possible pronouns.

Thanks to Harebrained Studios (now owned by Paradox Interactive), the makers of [BattleTech](https://store.steampowered.com/app/637090/BATTLETECH/).  BattleTech supports gender nonbinary characters as part of the base game, and is part of the inspiration for this mod.

Finally, thanks to the [Stellaris Modding Den](https://discord.gg/2qjkAF8DY7) for all the help with mod development.  Discussing Stellaris' built-in pronoun handling with another modder was my primary inspiration to create this mod.