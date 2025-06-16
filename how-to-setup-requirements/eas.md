# EAS

### Ethereum Attestation Service

Ethereum Attestation Service (EAS) is a decentralized protocol for creating and verifying attestations on Ethereum and other blockchains. Perfect for checking proof of attendance, certifications, memberships, or any verified credentials.

#### **Configure the requirement**

* In the role editor, click **"Add requirements"** and select **Ethereum Attestation Service**
* Set the verification parameters:
  * **Chain** - Select the blockchain where the attestation is stored (e.g., Arbitrum, Base, Ethereum)
  * **Reference** - Wallet address of the attester (the person/entity who issued the attestation)
  * **Schema ID** - Unique identifier for the attestation  (e.g., 0x1234...)
  * **Key** - The field name within the schema you want to verify (e.g., "rank", "status", "SelectionMethod")
  * **Value** - What that field must contain to qualify
* Choose matching logic:
  * **Equal** - Value must match exactly
  * **Doesn't equal** - Value must be anything except what you specify
  * **Includes** - Value must contain the specified text or be part of a list
* Customize the requirement name and image if you want
* Click **"Add requirement"**



Members connect their wallet and Guild automatically verifies their attestations on the specified blockchain.
