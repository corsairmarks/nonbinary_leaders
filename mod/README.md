# Overview

Would you like your leaders to have a chance to have gender identities that vary from the presentation of their portraits? Then this mod is for you!

The effects are more noticable for species portraits that have sexual dimorphism, but that is not a requirement.

# Changes

Stellaris supports 3 gender states in code (`male`, `female`, `indeterminable`), which correspond to the pronouns he, she, and they.  Whether a species uses binary male/female genders or the indeterminable gender is determined by its species class (e.g. molluscoid or fungoid).  This mod adds a chance for the binary species classes to have leaders adopt a new gender identity when they are spawned by the game (15% chance to consider changing their gender identity - 5% each to identify as indeterminable, female, or male).

Because Stellaris does not provide a scriptable way to check whether a species class is set to use binary genders or not, this mod uses a hard-coded list of species classes known to use binary genders in the unmodified game.  In addition, `gender = yes` is the default for custom species classes, so this mod assumes any unrecognized species classes are binary gendered.  What this means to you is that if you have a custom species class that is set to `gender = no` this mod will still think it is gendered and roll for a chance to change a leader's gender identity when they spawn.  It does not randomize the gender identity for the built-in species classes that are set to `gender = no`: fungoid, plantoid, lithoid, machine, robot, and all the crisis species.

This mod adds copious log entries to game.log file when running, so to see it working just check that log file.  Here's where you can find it: `%USERPROFILE%\Documents\Paradox Interactive\Stellaris\logs` (Windows), `~/Documents/Paradox Interactive/Stellaris/logs` (MacOS), `	~/.local/share/Paradox Interactive/Stellaris/logs` (*nix).

## Compatibility

This mod is implemented through an event attached to `on_leader_spawned` to add the % chance to reroll a leader's gender identity.  It should be widely compatible with other mods, including my other mods that also affect leader spawning ([Enable All Eligible Species Traits for Leaders](https://steamcommunity.com/sharedfiles/filedetails/?id=2499031295), [Scientist AI Assistant Upgrader](https://steamcommunity.com/sharedfiles/filedetails/?id=2498166286), [Full Military Service for Battle Thralls](https://steamcommunity.com/sharedfiles/filedetails/?id=2496357447)).

This mod is not compatible with achievements.

### Post-Game Start

This mod can be added or moved to your game safely without issue.  If you remove this mod, any leaders which already have had their gender identites set will remain as-is but new leaders will only spawn to match either binary genders or indeterminable genders depending on species class.

## Known Issues

None.

## Changelog

* 1.0.0 Initial version