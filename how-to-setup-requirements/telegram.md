# Telegram

Check if members belong to specific Telegram groups or channels.

**Setting up the Telegram requirement for groups:**

* In the role editor, click **"Add requirements"** and select **Telegram**
* Click **"Invite our bot"** and select your group
* Click **"Add bot as admin"** on Telegram (don't change permissions)
* Copy the **Group ID** of your Telegram group and paste it on Guild
* Select what to check from the dropdown options
* Add custom image and name for the requirement if you want
* Click **"Add requirement"**

<figure><img src="../.gitbook/assets/Add telegram.png" alt="Add telegram requirement "><figcaption></figcaption></figure>



**Setting up the Telegram requirement for channels:**

* In the role editor, click **"Add requirements"** and select **Telegram**
* Go to your Telegram channel
* Go to the channel settings, select the **Administrators** tab, and click **"Add Admin"**
* Add `@guildxyz_integration_bot` to the channel (don't change permissions)
* Once added, the Guild bot will send you a message within the channel with the Group ID
* Copy the **Group ID** from the bot's message and paste it on Guild
* Select what to check from the dropdown options
* Add custom image and name for the requirement if you want
* Click **"Add requirement"**



Members connect their Telegram account and Guild automatically verifies their membership status and selected attributes in the specified group or channel.
