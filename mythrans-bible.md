# The Mythran's Bible - A Server Operator's Guide to Darkflame Universe

So you've finally setup a server instance, created an admin account, then created additional accounts using the Account Manager. You've connected to the server using your client and everything seems to be working fine.

Now that you've reached this point, there's still a lot to know about managing and maintaining a server.

## Port Forwarding

The server you're running will need to open the following ports to allow for outside access to your server:

* 1001 - Auth Server
* 2000 - Master Server
* 2005 - Chat Server
* 3001 -
* 3007 -

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
    - Players at this level and above can spawn entities, instantly smash target players, run macros, and more.
    - **NOTICE:** This GM level should only be granted to trusted players.
* 9 - Server Operator: This level describes players with full access and permissions.
    - Players at this level can shut down the server.
    - **NOTICE:** This GM level should only be granted to system administrators.

## Console Commands

Here is a list of all console commands, sorted alphabetically and grouped by required permission level. Each level also has access to the commands of the levels above them. To run one of these console comands, enter them into chat.

### WORK IN PROGRESS

### 0 - Civilian

These commands are available to ALL normal players of the game, including newly created characters and non-moderators.

#### /pvp

**This is a custom command added by the Darkflame Server**

This command toggles a flag on the current player, which enables that player to attack, damage, and smash other players who are participating in PvP.

This system functions similarly to Terraria's PvP system; you must enable PvP in order to participate in it, and can disable it at any time.

### 9 - Server Operator

#### /shutdownuniverse

This command sends an announcement to all players that the server will be shut down for maintenance in 10 minutes, then shuts down the  the entire Darkflame Universe server.

#### /crash

This command immediately crashes the entire Darkflame Universe server, causing players to disconnect without advance warning.