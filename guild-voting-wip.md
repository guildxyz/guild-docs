---
description: Token weighted polls with Discord and Telegram.
---

# Guild Voting (WIP)

## Discord

You can create a new poll with Guild.xyz bot using the **`/poll` slash command** in one of the channels of your server.

It will prompt you in a DM to set up the poll:

![](<.gitbook/assets/image (15) (1).png>)

Firstly, you have to **choose the role and the requirement**. \
The role is the participating membership layer within your community, the requirement's token will be used for weighting. Keep in mind that the token-weighted voting only supports ERC-20 tokens.

![](<.gitbook/assets/image (5) (1) (1).png>)

![](<.gitbook/assets/image (2) (1).png>)

Now you have to **specify the question** of the poll:

![](<.gitbook/assets/image (3).png>)

In the next step you can **list the poll options and the reactions** (up to 20):

![](<.gitbook/assets/image (7) (1) (1).png>)

You can skip to the next step using the ** `/enough` slash command** (after you have successfully added 2 or more options).\
When you are done you will be prompted to **specify the expiration date** of the poll in the form of `dd:hh:mm` where _dd_ is the number of days, _hh_ is the number of hours and _mm_ is the number of minutes. Both `0:1:3` and `00:01:3` are valid inputs.

![](<.gitbook/assets/image (9) (1) (1).png>)

After specifying the date the bot will show you **how the poll will look like** when published:

![](<.gitbook/assets/image (6) (1) (1).png>)



You can use ** `/done` to accept** the poll as it is and publish to the channel. If you are not so sure about it you can still reset it using ** `/reset`** or even cancel with the ** `/cancel` slash command**.



## Telegram

The poll creation for Telegram is almost the same as on Discord. The bot will message you with all directions after hitting **`/poll` slash command,** these are the minor differences:

1. You **only have to choose the token** instead of both the role and requirement
2. We can't use Discord-like reactions for voting so you **only have to list the poll options**

![](<.gitbook/assets/image (18).png>)&#x20;

![](<.gitbook/assets/image (4) (1).png>)
