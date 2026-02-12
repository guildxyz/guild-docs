# Telegram group

Grant access to private Telegram groups automatically when members meet requirements. Perfect for gated communities, VIP channels, and holder-only discussions.



#### **Setting up Telegram group/channel rewards:**

* In the role editor, click **"Add reward"** and select **Telegram**
* Click **"Add bot to group or channel"** and select your group/channel&#x20;
* Add the Guild bot as an admin (don't change permissions)
* Once added, the Guild bot will send a message within the group with the **Group ID**
* Copy the **Group ID** of your Telegram group and paste it on Guild
* Click **"Add reward"**

\*You can add @guildxyz\_bot to your group directly on Telegram as well.

{% hint style="info" %}
The Guild bot must have admin permissions in your Telegram group to automatically add and remove members.
{% endhint %}

#### How Telegram group rewards work for members

* Members see the Telegram group reward but cannot join until they meet role requirements
* Once qualified, members click **"Join group"** to get automatic access to the group
* Access is granted immediately through the Guild bot
* If members lose role access, they are automatically removed from the Telegram group



#### Requirements for setup

* You must be an admin of the Telegram group or channel you want to gate
* The Guild bot must be added as an admin with proper permissions
* Your Telegram group must be set to **"Private"** (you can change this in your group settings under Group Type)

#### Bot commands for group management

You can use these commands in groups (channels have limited command visibility):

* **/start** - Welcome message with Group ID and instructions&#x20;
* **/help** - View documentation and support links
* **/status** - Check group status and configuration



#### Channel limitations

When using Telegram channels as rewards:

* **No command menu** - When you type "/", the command list won't appear automatically; you have to type /start /help or /status and hit enter
* **Bot must be admin** - The bot needs admin permissions with "Post messages" enabled
* **Setup required** - Make sure to add the bot through the "Add bot to channel" link, not the group link

#### Important notes

* The Guild bot (@guildxyz\_bot) handles both Telegram requirements and rewards
* If you previously used separate bots, they have been unified into @guildxyz\_bot
* The bot automatically manages member access based on role requirements - no manual intervention needed
* Group ID is automatically provided in the welcome message when you add the bot
* The bot status check verifies that your group is set to private and has proper permissions configured



