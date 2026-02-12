# Telegram

Check if members belong to specific Telegram groups or channels.



**Setting up the Telegram requirement for groups:**

* In the role editor, click **"Add requirements"** and select **Telegram**
* Click **"Invite our bot to your group"** and select your group
* Click **"Add bot as admin"** on Telegram (don't change permissions)
* Once added, the Guild bot will send a message within the channel with the **Group ID**
* Copy the **Group ID** of your Telegram group and paste it on Guild
* Select what to check from the dropdown options
* Add custom image and name for the requirement if you want
* Click **"Add requirement"**

\*You can add @guildxyz\_bot to your group directly on Telegram as well.

<figure><img src="../.gitbook/assets/Add telegram.png" alt="Add telegram requirement "><figcaption></figcaption></figure>



**Setting up the Telegram requirement for channels:**

* In the role editor, click **"Add requirements"** and select **Telegram**
* Click **"Invite our bot to your channel"** and select your channel
* Click **"Add bot as admin"** on Telegram (don't change permissions)
* Once added, the Guild bot will send a message within the channel with the **Group ID**
* Copy the **Group ID** of your Telegram channel and paste it on Guild
* Select what to check from the dropdown options
* Add custom image and name for the requirement if you want
* Click **"Add requirement"**



### Required permissions

If you added our bot through Guild, no action is needed. You only need to grant permissions if you manually added @guildxyz\_bot to your Telegram group or channel.

**For groups,** add the bot as an admin with these permissions:

* Ban users
* Invite users via link

**For channels,** add the bot as an admin with these permissions:

* Ban users
* Invite users via link
* Post messages (required for channels)

### Channel limitations

Telegram channels have some limitations compared to groups:

* **No command menu** - When you type "/", the command list won't appear automatically; you have to type /start /help or /status and hit enter
* **Bot must be admin** - The bot cannot see channel updates or respond unless it has admin permissions with "Post messages" enabled&#x20;
* **User experience** - You won't see available commands until the bot has proper admin permissions

### Bot commands

You can use these commands in groups (channels have limited command visibility):

* **/start** - Welcome message with Group ID and instructions&#x20;
* **/help** - View documentation and support links
* **/status** - Check group status and configuration

### How it works for members

Members connect their Telegram account and Guild automatically verifies their membership status and selected attributes in the specified group or channel.



### Important notes

* **Your Telegram group must be set to "Private"** - You can change this in your group settings under Group Type
* The bot status check includes verification that the group is set to private
* The same bot (@guildxyz\_bot) is used for both requirements and rewards
* If you previously used the old @guildxyz\_integration\_bot, it has been replaced by the unified @guildxyz\_bot
