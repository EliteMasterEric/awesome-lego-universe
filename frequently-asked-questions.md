# Frequently Asked Questions

This guide provides answers to frequently asked questions about LEGO Universe and Darkflame Universe.

## Why do I have to setup a server myself? Didn't the Darkflame Universe team say they were going to setup a hosted server?

Early this year, members of The LEGO Group (TLG) opened up discussions with the Darkflame Universe development team (DLU). Although we don't have all the information on what was discussed, we do know that TLG still cares about the game (especially the LEGO Games team). They love to see the enthusiastic community that still cares about it and appreciate the volunteer effort that has been continuing for the past decade to revive it.

TLG and DLU have been discussing possible courses of action to allow an "official unofficial" public server for about a year. If TLG did not want the project to succeed, they would have simply had their legal team send a letter and make DLU shut their project down (as has happened with many other attempts to revive long-dead MMOs).

Despite how much TLG may want to bring the game back, TLG has many overriding obligations that prevent them from condoning a public server. One major blocker is that there are legal restrictions to distributing old clients. Aside from containing copyrighted material (textures, models, and sound owned by TLG), they also contain code to handle physics, graphics, sound, networking, and other important stuff, that was written by third parties, and that TLG paid for permission to use, and these contracts lapsed a long time ago.

Another major blocker is that TLG has an incredibly high standard in terms of moderation. TLG has probably the best reputation of any toy company in the world (have you ever heard anyone say ANYTHING bad about LEGO aside from stepping on them?). A public server's moderation would have to be squeaky clean. If a young player logged into a DLU server and saw a giant phallus made of LEGO bricks on an in-game property, it would be TLG that would take the hit.

TLG and DLU have explored EVERY conceivable avenue, including but not limited to disabling chat and disabling user-generated content (i.e. properties) entirely. If you thought of it, DLU has likely proposed it. A public server is not viable at this time. This isn't because DLU doesn't want to do it, and it's not because TLG doesn't want to do it, and it's not because they didn't try as HARD as they could to get it to work.

Keep in mind, despite being written to interact with a proprietary program, [DarkflameServer](https://github.com/DarkflameUniverse/DarkflameServer) contains zero reverse engineered code. This means that it is 100% the property of the people who wrote it, the DLU team, and they have full rights to distribute it. Additionally, even if the repository does get taken down, dozens of people (including myself) have downloaded it already. LEGO Universe is back, and it is back forever.

Also keep in mind that DLU is still in talks with TLG, and it is imperative that these discussions are not sabotaged. You and a group of close friends can set up a server and play, but do NOT try to set up a large server for everyone to play on, and do not share your servers on public Discord servers or subreddits. If you do, you (and the rest of the community) may have to hear from TLG's lawyers.

## Can I install and use the client from my old CD?

You and many other players (myself included) have fond memories of the original game and have held onto the original disk for all that time. Sadly, the client included on the original disk contains a very early version of the game; it does not contain important bug fixes and content updates, such as the Nexus Tower and Crux Prime maps. Thus, it is not compatible with Darkflame Universe.

## Where can I get an updated client?

During the discussions with TLG, it has been concluded that TLG cannot allow major public forums to link to public clients. You will have to do your own research and find one.

You are looking for a LEGO Universe Client 1.10.64, unpacked. Try Google.

## How do I determine if my client is up-to-date? Is it safe, what if there's a virus?

These are very astute and excellent questions. There may be bad actors out there looking to capitalize on the new release who will upload a virus posing as an up-to-date client. I have [a guide on how to verify your client here](/verify-my-client.md).

## What does 'packed' or 'unpacked' mean? Does it mean compressed, like a ZIP file? How do I tell if my client is unpacked?

Every time TLG was ready to release an update to LEGO Universe, they took all the game's assets, models, and scripts, and combined them together into pack files. In order for Darkflame Universe to work, these files need to be unpacked.

An unpacked client can be distinguished by having a bunch of extra folders, such as `scripts` and `maps`, within the `res` folder of your client.

If your client is not unpacked, []

## Help! I started Avant Gardens Survival and the play button doesn't appear! I can't move!

This is actually a bug with the script in the client, and you will need to edit that script in order to fix it.

Log out, close your game, [follow this guide to the letter](https://github.com/DarkflameUniverse/DarkflameServer#survival), then 

## Help! Mechs in Avant Gardens aren't dropping the Turret quick-builds!

Your server's `CDServer.sqlite` file was not configured correctly. [Follow this guide to learn more](https://github.com/DarkflameUniverse/DarkflameServer/issues/46).

## Can I stream the game on Twitch?

Twitch has a section of their community guidelines which reads:

> Intellectual Property Rights
> You should only share content on your Twitch channel that you own, or that you otherwise have rights to or are authorized to share on Twitch. If you share content on your Twitch channel that you do not own or otherwise do not have the rights to share on Twitch, you may be infringing another person’s intellectual property rights. 
> Examples of content you should not share on Twitch without permission from the copyright owners or unless otherwise permitted by law include:
> Pirated games or content from **unauthorized private servers**

Note the bold text; Darkflame Universe is technically an unauthorized private server. I won't straight-up say that you can't, but streaming the game, consider the risks to yourself, and whether you okay with potentially receiving a copyright strike on your account.

## Can Darkflame Universe be modded? Can I new items? New skills? New enemies? New missions and worlds?

The short answer is yes. The long answer is no.

Basically all the work done since the game was shut down has been focused on getting the base game functional. That work is now done, and the team has come away with a good understanding of how many of the systems in the game work. Now that DLU is out, new tools will hopefully be developed (such as a modloader or patcher) to allow for new content to be added to the game.

All the things I listed (new items, new skills, new enemies, new missions, new worlds) have the capability to be added to the game, but none of the work to enable modding support has been done. Thankfully, with the release of a fully functional server, the community will likely see a major surge of attention and talent to assist in this effort.

However, there is one thing to note. There is a tool called HappyFlower, which is an old level editor. It only works on the alpha version of the game, which means it doesn't support adding enemies, NPCs, or missions, but it does allow you to edit and create new worlds. In the future, other important features will be added, and users will eventually be able to create their own content, similar to worlds like Moonbase and Portabello.