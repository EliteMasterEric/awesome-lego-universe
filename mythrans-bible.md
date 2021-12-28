# The Mythran's Bible - A Server Operator's Guide to Darkflame Universe

So you've finally setup a server instance, created an admin account, then created additional accounts using the Account Manager. You've connected to the server using your client and everything seems to be working fine.

Now that you've reached this point, there's still a lot to know about managing and maintaining a server.

## Port Forwarding

The server you're running will need to open the following ports to allow for outside access to your server|

* 1001 - Auth Server
* 2000 - Master Server
* 2005 - Chat Server
* 3000-4000 - 

If you're using ufw as a firewall (most firewalled Linux systems), this can be done with:
```
sudo ufw allow 1001/udp
sudo ufw allow 2000/udp
sudo ufw allow 2005/udp
sudo ufw allow 3000:4000/udp
```

## GM Levels

Game moderator levels define what console commands a given account has access to in-game.  To modify a player's maximum GM level, set the `gm_level` column in the `accounts` table in the MySQL database.

Players have a max GM level and a current GM level; at any time, a player can use the `/setgmlevel` command to raise their current GM level up to their maximum, which grants them permissions corresponding with that level, or lower their GM level down to a lower level, or 0, which limits what commands they can execute.

A player with full GM permissions can lower themselves down to 0 to play the game as though they were a normal player, then raise their level up if they need to do something like teleport or unstuck themselves. Think of it like Minecraft; if you have permissions, you can play the game in Survival, and call `/gamemode creative` only when you get stuck.

There are 10 total levels, as follows:

* 0 - Civilian: This level describes all normal players of the game.
    - Players at this level still have access some commands, see the Console Commands section below.
* 1 - Forum Moderator: This level describes forum moderators who have very few permissions.
    - **NOTICE:** Players with their GM level set to this level and above may experience deviations from normal gameplay.
    - Players at this level can send any messages in chat without moderation or blacklist checking.
        - This is based on your current level, not your maximum level, so if you are currently playing as a Civilian you cannot chat without filters.
    - Players at this level and above will appear as Mythrans. This cannot be toggled at this time.
* 2 - Junior Moderator: This level describes moderators who can help regulate chat.
    - Players at this level and above can access chat logs, kick players, and mute players.
    - Players at this level and above can teleport to specific coordinates on the map.
* 3 - Moderator: This level describes moderators who can help deal with glitches.
    - Players at this level and above can return lost items to players.
* 4 - Senior Moderator: This level describes moderators who can help deal with problematic players.
    - Players at this level and above can ban players.
* 5 - Lead Moderator: This level describes moderators who are trusted to manage user-generated content.
    - Players at this level and above can approve properties.
* 6 - Junior Developer: This level describes junior developers and members of future content teams.
    - On live servers, their GM level is reset to 0 (Civilian).
* 7 - Inactive Developer: This level describes inactive developers with limited permissions.
* 8 - Active Developer: This level describes players who have been granted all but the most powerful permissions.
    - Players at this level and above can spawn entities, instantly smash target players, send Mythran announcements to all players, run macros, and more.
    - **NOTICE:** This GM level should only be granted to trusted players.
* 9 - Server Operator: This level describes players with full access and permissions.
    - Players at this level can shut down the server.
    - **NOTICE:** This GM level should only be granted to system administrators.

## Console Commands

Here is a list of all console commands, grouped by required permission level. Each level also has access to the commands of the levels above them. To run one of these console comands, enter them into chat.

Values in `<brackets>` represent necessary parameters, values in `(parens)` represent optional parameters.

### WORK IN PROGRESS

### 0 - Civilian

These commands are available to ALL normal players of the game, including newly created characters and non-moderators.

#### /pvp

**This is a custom command added by the Darkflame Server**

This command toggles a flag on the current player, which enables that player to attack, damage, and smash other players who are participating in PvP.

This system functions similarly to Terraria's PvP system; you must enable PvP in order to participate in it, and can disable it at any time.

#### /playanimation <anim-name>

This command triggers the player to play an animation with the given internal name. This can look somewhat buggy, since any player animation can be played, such as attacks that don't match your current gear, but isn't that part of the fun is it?

**TODO: Add a curated list of some fun animations.**

#### /playanim <anim-name>

Alias for `/playanimation`.

#### /die

This command smashes the current player, prompting them to respawn.

#### /resurrect

This command smashes the current player and respawns them.

**TODO: How does this differ from `/die`?**

#### /who

This command outputs a list of all the players in the current instance.

#### /ping (-l)

This commands outputs your average ping level, indicating the strength of your connection to the server. Use `/ping -l` to output your latest ping level rather than your average ping level.

#### /skip-ags

This command will check if the player has been assigned mission ID `229`, and will skip it if they have.

This mission ID corresponds to the required mission in which the player must survive one minute in Avant Gardens Survival. Since this minigame can sometimes be buggy, this command will allow any player to skip the mission if needed.

#### /fix-stats

**TODO: This command's purpose is unknown.**

#### /requestmailcount

This command will show the `You have x new messages` status box at the bottom right corner of your game screen.

#### /instanceinfo

**TODO: What does this do?**

#### /credits

Displays information about the developers of Darkflame Universe.

#### /info

Displays basic information about the currently connected Darkflame Universe server.

#### /leave-zone

**TODO: This requires clarification.**

Moves the current player out of an instanced zone. Such as the Block Yard or a Minigame such as Avant Garden Survival

#### /join <password>

**TODO: This requires clarification.**

Moves the player to a private instance.

### 2 - Junior Moderator

#### /mute <name> (days) (hours)

Mutes the target player for the target number of days plus the target number of hours.

If no duration is specified, the mute is permanent.

#### /kick <name>

Kicks the target player from the server. They can still login again.

#### /ban <name>

Bans the target player permanently from the server. They cannot login again.

At this time there is no easy functionality to unban a player.

#### /teleport  <x> (y) <z>

Teleports to the given X and Z coordinates. If Y is specified, the player will be teleported to that height; otherwise, the player will be teleported to the height of the terrain.

#### /tele

Alias for `/teleport`.

### 3 - Moderator

#### /mailitem <name> <item>

Sends an item to the mailbox of the target player.

### 5 - Lead Moderator

#### /approveproperty

Approves the currently accessed user-built property for public viewing.

### 8 - Active Developer

#### /kill <user>

https://www.youtube.com/watch?v=dyIilW_eBjc

#### /speedboost <boost>

Boost the player's speed by the given amount.

**TODO: Does this support decimal values or only whole numbers?**

#### /freecam

| Key     | Description                                  |
|---------|----------------------------------------------|
| Q/E     | Rotates the camera by the X axis. Left-Right |
| R/F     | Moves the camera up and down the Y axis      |
| W/A/S/D | Moves the camera by the X / Z Axis           |
| Mouse   | Rotate the camera by X / Y / Z               |

Toggles free camera mode.
    
**TODO: Expand description.**

#### /setcontrolscheme

**TODO: What does this do?**

#### /list-spawns

**TODO: What does this do?**

#### /unlock-emote

**TODO: What does this do?**

#### /setuistate <state>

**TODO: What does this do?**

#### /toggle <visible>

**TODO: What does this do?**

#### /setinventorysize <size>

Sets the size of the current player's inventory to the specified value.

#### /setinvsize <size>

Alias for `/setinventorysize`.

#### /runmacro <path>

Runs the specified macro at the path `./res/macros/<path>.scm`.

#### /addmission <mission-id>

Forces the current player to accept the mission with the specific ID.

#### /completemission <mission-id>

Immediately completes the mission with the specific ID for the current player.

#### /setflag <flag-id>

Every player has a 12,008-bit string associated with them that contains a large number of on-off switches associated with the character's status and progress. This command enables a specific flag on the current player.

[List of known flags](https://docs.lu-dev.net/en/latest/game-mechanics/flag-system.html#known-flags).

#### /clearflag <flag-id>

Every player has a 12,008-bit string associated with them that contains a large number of on-off switches associated with the character's status and progress. This command disables a specific flag on the current player.

[List of known flags](https://docs.lu-dev.net/en/latest/game-mechanics/flag-system.html#known-flags).

#### /resetmission <mission-id>

Sets a completed mission back as active.

#### /playeffect <effect-id>

Starts playing a specific effect on the given player.

#### /stopeffect <effect-id>

Stops playing a specific effect on the given player.

#### /setanntitle <title>

Set the title of the next announcement to send.

#### /setannmsg <message>

Set the message of the next announcement to send.

#### /getnavmeshheight

**TODO: What does this do?**

#### /gmadditem <id> (count)

Gives this player an item based on its ID. Optionally specify the quantity of the item to give.

See [Notable Item IDs](#notable-item-ids) for a list of some of the item IDs you can use.

#### /announce

Send an announcement to all members of the server. You need to call `/setanntitle` and `/setannmsg` first to set the title and description of the message.

#### /setname <name>

Set the current player's name.

**TODO: Is this permanent or what?**

#### /title <title>

Set the current player's title (their name will display as `Name - Title`).

#### /tpall

Teleport all other players to the current player's position.

#### /dismount

Forcibly dismount the player from their vehicle or mount.

#### /buffme

Grants the player 999 Health, Armor, and Imagination.

#### /startcelebration

**TODO: What does this do?**

#### /buffmed

Grants the player 9 Health, Armor, and Imagination.

#### /refillstats

Refills the player's Health, Armor, and Imagination back to full.

#### /lookup <name>

**TODO: What does this do?**

Looks up a player by name and ???

#### /spawn <entity-id>

Spawns an entity of the given ID.

**TODO: Add IDs for certain common entities.**

#### /giveuscore <amount>

Gives a certain amount of UScore to the current player. They will likely level up because of this.

#### /pos

Prints out the current player's X, Y, and Z position.

#### /rot

Prints out the current player's W, X, Y, and Z rotation.

#### /locrow

Prints out the current player's X, Y, and Z position, and their W, X, Y, and Z rotation.

#### /playlvlfx

**TODO: What does this do?**

#### /playrebuildfx

**TODO: What does this do?**

#### /freemoney <amount>

Gives the current player the specified amount of coins.

#### /setcurrency <amount>

Sets the current player's wallet to the specified amount of coins.

#### /gminvis

Toggles the current player's invisiblity.

#### /gmimmune

**TODO: What does this do?**

#### /buff <id> <duration>

Grants a specified buff for a given duration.

**TODO: Is the duration in seconds?**

**TODO: Build a list of common buffs and debuffs.**

#### /testmap <zone> (force)

Attempt to transport the player to the given zone.

Use `/testmap <zone> force` to forcibly teleport to a potentially invalid zone. Can have disastrous results.

See [Available Zone IDs](#available-zone-ids) for a list of zone IDs you can use.

#### /createprivate

**TODO: What does this do? Does it have to do with `/join` ?**

#### /debugui

Open the debug UI./testmap

#### /boost

**TODO: What does this do?**

#### /activatespawner <name>

Activate one or more spawners by name.

#### /spawnphysicsverts

**TODO: What does this do?**

#### /reportproxphys

**TODO: What does this do?**

#### /triggerspawner

**TODO: What does this do?**

#### /inspect

**TODO: What does this do?**

#### /reforge <base> <target>

Attempts to create a "reforged" item, which has the appearance of one item and the stats of another.

**DO THIS AT YOUR OWN RISK, VERY BUGGY.**

#### /config-get <name>

Gets a configuration value.

#### /config-set <name> <value>

Sets a configuration value.

**TODO: Make a list of common configuration values.**

#### /metrics

Output a list of server metrics.

### 9 - Server Operator

#### /shutdownuniverse

This command sends an announcement to all players that the server will be shut down for maintenance in 10 minutes, then shuts down the  the entire Darkflame Universe server.

#### /crash

This command immediately crashes the entire Darkflame Universe server, causing players to disconnect without advance warning.

## Available Zone IDs

Below is a list of all of the zones accessible in the base game. Developers can warp to any zone with the `/testmap <id>` command.

ID | Name
---|---
1000|Venture Explorer
1001|Return to Venture Explorer
1100|Avant Gardens
1101|Avant Gardens Survival
1150|Block Yard
1151|Avant Grove
1200|Nimbus Station
1201|Pet Cove
1204|Battle of Nimbus Station
1250|Nimbus Rock
1251|Nimbus Isle
1300|Gnarled Forest
1302|Cannon Cove Shooting Gallery
1350|Chantey Shanty
1400|Forbidden Valley
1402|Forbidden Valley Dragon Battle
1403|Dragonmaw Chasm Racetrack
1450|Raven Bluff
1600|Starbase 3001
1601|DeepFreeze
1602|Robot City
1603|MoonBase
1604|Portabello
1800|Crux Prime
1900|Nexus Tower
2000|Ninjago Monastery
2001|Battle Against Frakjaw

## Notable Item IDs

Below is a list of item ids for notable items.

ID|Name
---|---
1727|Jetpack
