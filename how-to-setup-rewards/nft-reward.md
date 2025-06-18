# NFT reward

Create and distribute custom NFTs to role members. Perfect for proof-of-participation, collectibles, community credentials, or exclusive access tokens with real onchain utility.

#### Setting up NFT rewards

**1. Create the NFT**

* In the role editor, click **"Add reward"** and select **NFT**
* Upload NFT image (JPG, PNG, or GIF, up to 100MB)
* Add NFT name and metadata description (optional)
* Set metadata attributes (rarity, level, season, etc.) - optional
* Choose transferability: **Non-transferable (Soulbound)** or **Transferable**\


**2. Configure supply and claiming**

* Set supply: **Unlimited** or **Limited** with a maximum number
* Set claim limits per wallet address
* Configure claiming time window (start and end dates)
* Choose supported blockchain from dropdown\


**3. Set pricing and payout**

* Set mint price or leave it zero for free minting
* Configure payout address (defaults to your connected wallet)
* Note: small Guild minting fee applies\


**4. Deploy NFT**

* Click **"Create NFT reward"** to deploy the contract onchain
* Only members who meet the role's requirements can claim the NFT
* Click **"Collect NFT"** to see contract details and top collectors

{% hint style="info" %}
Each NFT can only be attached to a single role.
{% endhint %}

#### How NFT rewards work for members

* Members see the NFT reward but cannot claim until they meet role requirements
* Once qualified, members click **"Collect NFT"** to mint the NFT to their wallet
* Minting happens onchain and requires gas fees
* NFTs appear in member wallets and automatically list on OpenSea
* Metadata updates dynamically reflect on already minted NFTs

Unlike other rewards, members keep their NFTs permanently even if they lose role access, since the NFT is already minted onchain.
