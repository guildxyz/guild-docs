# NFT Balance

Check whether members hold specific NFTs or quantities of NFTs on a selected blockchain. Perfect for token-gated access, exclusive holder benefits, or tiered membership based on collection size.



**Setting up NFT balance requirements:**

* In the role editor, click **"Add requirements"** and select **NFT Balance**
* Fill out the parameters:
  * **Chain** - Select the blockchain where the NFT contract is deployed
  * **Token address** - The contract address of the NFT collection you're checking
  * **Token ID** - Enter the unique identifier of a specific NFT, or leave blank to check general ownership of any NFT from this collection
  * **Balance** - Specify how many NFTs a member must hold using these conditions:
    * **Equal** - Must hold exactly the specified number
    * **Doesn't equal** - Must hold any number except the one specified
    * **Greater than** - Must hold more than the specified number
    * **Greater than or equal to** - Must hold at least the specified number
    * **Less than** - Must hold fewer than the specified number
    * **Less than or equal to** - Must hold at most the specified number
    * **Range** - Must hold a number within the specified range
* Customize the requirement name and image if you want
* Click **"Add requirement"**

Members connect their wallet and Guild automatically checks their NFT holdings on the specified blockchain. If someone sells their NFT and no longer meets the requirement, they automatically lose access to the role.

