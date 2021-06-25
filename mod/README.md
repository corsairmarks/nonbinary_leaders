# Overview

Would you like your leaders to have a chance to have gender identities that vary from the gender presentation of their portraits?  Do you want your leaders to be able to use "they" pronouns?  Then this mod is for you!

The effects are more noticable for species portraits that have sexual dimorphism, but that is not a requirement.

# Changes

Stellaris supports 3 gender states in code (`male`, `female`, `indeterminable`), which correspond to the pronouns he, she, and they.  Whether a species uses binary male/female genders or the indeterminable gender is determined by its species class (e.g. molluscoid or fungoid).  This mod adds a chance for the binary-gendered species classes to have leaders adopt a new gender identity when they are spawned by the game (24% chance to consider changing their gender identity - 8% each to identify as indeterminable, female, or male).

With this mod, leaders of a binary-gendered species who become indeterminable have a 50/50 chance of presenting as feminine or masculine, and leaders who become female/male (or do not change from their starting gender) have a 10% chance to present as the opposite gender in their portrait.  In order to implement this effect, it was necessary to redefine the portrait groups associated with each species.

What this means to you is that most leader portrait mods will need a compatibility patch in order to properly respect the leader's gender presentation flag.  Without a patch, males will always present as masculine, females will present as feminine, and indeterminables will present as the default for the species.  Fun fact: some built-in species use the female portrait as default, but most use male.

Because Stellaris does not provide a scriptable way to check whether a species class is set to use binary genders or not, this mod uses a hard-coded list of the built-in species classes known to use binary genders.  In addition, `gender = yes` is the default for custom species classes, so this mod assumes any unrecognized species classes are binary-gendered.

What this means to you is that if you have a custom species class that is set to `gender = no` this mod will still think it is gendered and roll for a chance to change a leader's gender identity when they spawn.  It does not randomize the gender identity for the built-in species classes that are set to `gender = no`: fungoid, plantoid, lithoid, machine, robot, and all the crisis species.

This mod optionally adds copious log entries to game.log file when running; use the in-game console to enable it with `effect set_global_flag = nonbinary_leaders_enable_tracing`.  Here's where you can find the game.log file: `%USERPROFILE%\Documents\Paradox Interactive\Stellaris\logs` (Windows), `~/Documents/Paradox Interactive/Stellaris/logs` (MacOS), or `~/.local/share/Paradox Interactive/Stellaris/logs` (*nix).  To turn tracing off again, issue this command on the in-game console: `effect remove_global_flag = nonbinary_leaders_enable_tracing`.

Lastly, you can log detailed information about all of your leaders (owned and pool) to game.log by firing my debugging event from the in-game console: `event nonbinary_leaders.1000`.  I used this to help undestand the game state while developing and decided to leave it available for future use.

## Compatibility

This mod is implemented via an event attached to `on_leader_spawned` to add the % chance to reroll a leader's gender identity.  That part should be widely compatible with other mods, including my other mods that also affect leader spawning ([Enable All Eligible Species Traits for Leaders](https://steamcommunity.com/sharedfiles/filedetails/?id=2499031295), [Scientist AI Assistant Upgrader](https://steamcommunity.com/sharedfiles/filedetails/?id=2498166286), [Full Military Service for Battle Thralls](https://steamcommunity.com/sharedfiles/filedetails/?id=2496357447)).

As discussed above, a compatibility patch is necessary to fully support varying gender presentation for other mods that add species portraits.  By default, this mod supports all the built-in, gendered species classes and any sexually dimorphic species in each class.

If you would like me to implement a compatibility patch (to support feminine/masculine presentation from sexual dimorphism and/or to respect a custom species class as non-gendered), please leave a comment asking nicely, what you want, and with a link to the mod you want to be compatible.

This mod is not compatible with achievements.

### Post-Game Start

This mod can be added to or removed from your savegame safely without issue.  If you remove this mod, any leaders which already have had their gender identities set will remain as-is but new leaders will only spawn to match either binary genders or indeterminable genders depending on species class.  Leader portraits will revert to the default selection criteria.  Although leaders retain any custom flags set on them, this doesn't affect gameplay.

## Known Issues

### Unresolvable Issues

If you recruit a leader while paused, and the newly-created replacement in the leader pool has changed their gender identity, you may see two leaders by the same name in the leader pool.  Unpause the game and the duplicate will be removed.  If you have the "Recruit Leader" window open when the duplicate is removed, you will see the leader's portrait change clothes (to the defaults) and their level become -1.  This is purely a display issue - that leader has been removed.  If you never hire leaders while paused, or if you close the "Recruit Leader" window before resuming the game, you will not experience this graphical glitch.  This graphical glitch also leads to lots of leader-related logs in error.log - most of which are because the removed duplicate leader has no owner, and thus some triggers related to their portrait's clothing break until the game finishes removing the leader.

### Limitations

Only leaders that are spawned into the leader pool (whether the pool is for a player or an AI) will have a chance to randomize their gender identity and presentation.  Leaders created through other means (for example, the `create_leader` and `clone_leader` effects) are unaffected.  Generally those are special event leaders and are intended to have a particular gender.

Leaders which select to identify as nonbinary (`indeterminable`) will not show a gender in their tooltip.  This is as-designed by Paradox, because the original purpose of the third gender is for non-gendered species (i.e. has no concept of gender at all).  Showing the line "Gender: Indeterminable" for every one of their leaders would be redundant.

Finally, it is not possible to allow for selecting gender-nonbinary rulers during species creation.  The logic for the species customization screens is part of the core Stellaris game and is not alterable by modders.

## Changelog

* 1.0.0 Initial version

## Source Code

[Hosted on Github](https://github.com/corsairmarks/nonbinary_leaders)

### Development Notes

It is best to clone this repository into `<Stellaris User's Directory>/Paradox Interactive/Stellaris/mod`, and then make a connection to the `mod` folder via a `*.mod` file's `path` property.  That will ensure the game can see the files, and also that CWTools will parse them.  Also note that the README.md file exists in the `mod` directory but is symbolically linked in the root directory.

# Request for Collaboration

I'm looking for one or more people knowledgable about modding portraits and models for Paradox games.  With my newly-discovered ability to unlink the in-game gender of a leader from their appearance, I want to create some additional options for the human portrait set.  Notably, I'd like to have more variability in gender presentation of the portraits.  The existing portraits only offer feminine and masculine presentation.

# Special Thanks

Thanks to Paradox Development Studios (a subsidiary of Paradox Interactive) for making [Stellaris](https://store.steampowered.com/app/281990/Stellaris/), a game that I have enjoyed playing and modifying.  This mod would not be possible without their efforts to add aliens which do not use a gender - a feature I repurposed for this mod!  They did all the heavy lifting to make their localisation (translations) work with 3 possible pronouns.

Thanks to Harebrained Studios (now owned by Paradox Interactive), the makers of [BattleTech](https://store.steampowered.com/app/637090/BATTLETECH/).  BattleTech supports gender nonbinary characters as part of the base game, and is part of the inspiration for this mod.

Finally, thanks to the [Stellaris Modding Den](https://discord.gg/bHVez2C) for all the help with mod development.  Discussing Stellaris' built-in pronoun handling with another modder was my primary inspiration to create this mod.