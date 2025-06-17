# Token balance

Check whether members hold a certain amount of tokens on a selected blockchain. Perfect for creating token-gating access and tiered memberships.



**Setting up token balance requirements:**

* In the role editor, click **"Add requirements"** and select **Token Balance**
* Fill out the parameters:
  * **Chain** - Select the blockchain where the token is deployed
  * **Token address** - The contract address of the token you want to check
  * **Balance** - Specify how many tokens members must hold using these conditions:
    * **Equal** - Must hold exactly the specified amount
    * **Doesn't equal** - Must hold any amount except the one specified
    * **Greater than** - Must hold more than the specified amount
    * **Greater than or equal to** - Must hold at least the specified amount
    * **Less than** - Must hold fewer than the specified amount
    * **Less than or equal to** - Must hold at most the specified amount
    * **Range** - Must hold an amount within the specified range
* Customize the requirement name and image if you want
* Click **"Add requirement"**

Members connect their wallet and Guild automatically checks their token holdings. If someone sells their tokens and no longer meets the requirement, they automatically lose access to the role.
