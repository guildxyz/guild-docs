---
description: A guide on how to protect your Discord community.
---

# Guild Guard

## What's Guild Guard?

Guild Guard is a Web3 CAPTCHA to combat bots with the power of Ethereum. It provides full protection against Discord scams acting like a security layer on your server. With the activated Guard, bad actor bots won't see any channels or members of your community on your Discord. No more unwanted messages, phishing attacks, DM scams and announcement channel posts impersonating moderators.

## Setting up the Guard

### Adding the Guard to your Discord server

To protect your community, you can add the Guild Guard to your Discord server easily by the following link: [https://guard.guild.xyz/](https://guard.guild.xyz/)

_Note: If you're already a guild owner or admin, you can set it up on your guild's page at the ‘Edit Guild - Security’ section also._

### Entry Channel

The channel where those need to authenticate themselves via the Guild.xyz bot:

* who join your Discord through an invite link after you set up the Guild Guard, and
* who joined your server before the Guard, but either doesn’t have any role or between the 2 security level setups you chose to authenticate your existing members with roles also.\
  _Note: More info under section 'Security Levels'_

You have 2 options to choose from when setting up the entry channel:

1. **Creating a new channel**\
   ****The new channel will be named ‘entry-channel’ automatically.
2. **Choosing an already existing one**\
   ****At this channel the ‘View channel’ will be enabled for the role @everyone

_Note: The entry channel is only visible to the server owner, accounts with administrator permission and those who haven't yet authenticated._

__![](<../.gitbook/assets/image (12).png>)__

### Security Levels

As mentioned before, you have the freedom to decide between two security levels when you set up the Guard:

1. **Authenticating existing members:**\
   ****Everyone on your server must be authenticated by the Guild.xyz bot to regain access to your Discord, regardless of whether they already have a role or not.\
   _Note: By verifying, everyone joins your guild and gets a free entry ‘Member’ role._
2. **Keeping access to existing members:**\
   ****Those who already have a role don't have to authenticate, they don't lose their server access. In short: Everyone with a role is protected by the Guild Guard.\
   _Note: Although those who already have a role can access your server, they won't become members of your guild until they authenticate themselves._

![](<../.gitbook/assets/image (9).png>) ![](<../.gitbook/assets/image (10).png>)

_Note: ETH-compatible chains are also supported for authentication, you just need an EVM address for connecting your wallet. Click_ [_here_](https://docs.guild.xyz/guild/blockchains-supported) _to check out the supported blockchains._\
__

**The key difference between the security levels:**\
****If you choose to authenticate your existing members, only people with roles set up your guild can access your server, while if you choose to keep access to existing members, people with any role keep their access to your Discord.

_Note: In the second scenario, if admins create an entirely new role on Discord after setting up the Guard, accounts with that new role only won't be guarded (unless admins manually change the settings and channel permissions)._

### Signing to submit on [guard.guild.xyz](https://guard.guild.xyz/)

By hitting the ‘Submit’ button, you create a guild with the same name as your Discord server, and it will automatically have a free entry 'Member' role.

## The key to magic

In the entry channel, the newly joined and unauthenticated accounts can only see:

* The server owner,
* The members with admin rights,
* The good-intention bots, and
* The other unauthenticated users.

**The magic behind:**\
****The reason unauthenticated accounts can't see your members on the entry channel is because everyone who's already verified cannot see that channel either. It's because in the permissions settings the @everyone role is set to not see anything but the entry channel = the 'View Channel' is enabled for that only.

_Note: When people verify themselves on the entry-channel and become a member of your guild with a role, they won’t be able to see that channel anymore and those who are not verified._

**Disclaimer: Discord refresh ‘bug’**\
****Channels are updated before you press the button, but users are not updated immediately, only if you switch to another channel. After then you cannot switch back to the entry channel unless you leave the guild in the interface, because you will be stripped of your role and put back into quarantine.
