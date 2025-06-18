# Discord role

Grant Discord server roles automatically when members meet requirements. Perfect for creating tiered access, exclusive channels, and community recognition.

#### Setting up Discord role rewards

**1. Connect your Discord server**

* In the role editor, click **"Add reward"** and select **Discord**
* Select your Discord server from the already added server list
* Or add a new one (see Discord setup guide: [how-to-add-discord.md](../how-to-add-discord.md "mention"))
* Create a new Discord role or select an existing Discord role
* Click **"Add reward"**

{% hint style="info" %}
The Guild bot must be on your selected Discord server to assign/remove roles. See how to add the Guild bot to your server here: [how-to-add-discord.md](../how-to-add-discord.md "mention").
{% endhint %}

#### How Discord role rewards work

* Members see the Discord role reward but cannot claim it until they meet requirements
* Once qualified, members click **"Claim"** to receive the Discord role
* Role assignment happens automatically but may take 1-2 minutes due to Discord rate limits
* Members see a timer showing estimated assignment time during busy periods
* If members lose role access, the Discord role is automatically removed

#### Requirements for setup

* Guild bot must be added to your Discord server with "Manage Roles" permission
* The Guild bot's role must be positioned higher than roles it needs to assign
