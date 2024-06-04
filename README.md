# L4D2_Max_Common_Spawn
**Alliedmodders**: https://forums.alliedmods.net/showthread.php?t=347871

Attempts to clamp the amount of common infected alive at any one time to `z_common_limit` cvar. By game default this is 30, and this plugin uses an added leniency of 5.

When the amount of common infected alive is greater than the default `z_common_limit` + leniency, a timer (3.0 seconds) is created. When that timer expires, common infected over the `z_common_limit` will be deleted and a **second timer** is created. During that second timer, any common infected that spawn that would push the count of common infected over the `z_common_limit` will be deleted. If no deletions have taken place after the set amount of time (5.0 seconds), then the plugin will stop deleting common infected. It will revert back to it's default state of watching for `z_common_limit` + leniency amounts.

#### Plugin commands:
- `sm_common_amt` Prints the status of plugin, as well as current / max common infected.

#### Todo:
- [ ] \(Optional) Use kill flags instead of entity deletion.
- [ ] \(Optional) Loop from highest entity count instead of lowest entity count on initial loop.

# Notes
Since this plugin does not instantly delete common infected when they spawn initially, this can create a jarring effect where common infected are deleted in the player's vision if they are over the `z_common_limit` when the first timer initially expires. Keep in mind, that the game's `OnEntityDestroyed()` takes about a second in realtime to be called on a common infected that was killed.

# Reason
Some custom campaigns in Left4Dead 2, noteably older ones, will use map triggers to forcibily spawn common infected. If the survivors are unable to kill zombies fast enough, this will slowly begin to result in a large amount of common infected on the map. Since there is no limit to how many common infected these maps could spawn, this essentially means you'll have infinite common infected.

However, campaigns that don't use map triggers to force spawn common infected should not be affected by this plugin. The game's AI director when it spawns a horde will occasionally spawn common infected 2 or even 3 higher than the `z_common_limit`. Since this plugin uses a leniency of `5`, this shouldn't be a problem. In theory, you could lower the leniency to `4`, and possibly `3` but that could be risky.

# Credit
This plugin is a modified version of Silver's plugin. As well as general assistance in the Alliedmodder's Discord.