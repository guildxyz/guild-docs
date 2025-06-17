# Farcaster

Check Farcaster activity and profile attributes to gate access based on social engagement, profile completeness, or specific following relationships.

#### Setting up Farcaster requirements

**Have at least \[x] followers:**

* In the role editor, click **"Add requirements"** and select **Farcaster**
* Choose **Have at least \[x] followers**
* Set the follower count condition using:
  * **Equal** - Exactly this number of followers
  * **Doesn't equal** - Any number except the one specified
  * **Greater than** - More than the specified number
  * **Greater than or equal to** - At least the specified number
  * **Less than** - Fewer than the specified number
  * **Less than or equal to** - At most the specified number



**Follow a profile:**

* Choose **Follow a profile**
* Enter the **Target FID** of the account they must follow
* Check the box if they must follow this account, or uncheck if they must NOT follow it



**Have something in your profile:**

* Choose **Have something in your profile**
* Select which profile field to check:
  * **Bio** - Check if their bio contains specific text
  * **FID** - Check for a specific Farcaster ID
  * **Username** - Check for a specific username
  * **Display name** - Check for a specific display name
* Choose matching logic: **Equal**, **Doesn't equal**, or **Includes**



For all requirements, customize the requirement name and image if you want, then click **"Add requirement"**.

Members connect their Farcaster account and Guild automatically verifies their profile data and social activity.
