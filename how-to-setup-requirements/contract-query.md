# Contract query

Check if a smart contract method returns specific values when called. Perfect for verifying custom onchain conditions, protocol holdings, or complex smart contract states.

\
**Setting up Contract Query requirements:**

* In the role editor, click **"Add requirements"** and select **Contract query**
*   Fill out the parameters:

    * Select the **Chain** where your contract is deployed
    * Enter the **Contract address** you want to query
    * Choose the contract **Method** from the dropdown (Guild automatically fetches available methods from the contract ABI)
    * Fill in the **Input parameters** - Guild shows the exact fields needed with names, types, and indexes
    * Select **Output to check** - choose which return value from the contract method to verify
      * **Output index** - Smart contract methods can return multiple values. The index (0, 1, 2, etc.) specifies which returned value to check:
        * Index 0 = first returned value
        * Index 1 = second returned value
        * Index 2 = third returned value, and so on\

      * **Output types:**
        * **Output bigint** - Large numbers (token balances, timestamps, counts, IDs)
        * **Output address** - Wallet addresses or contract addresses
        * **Output boolean** - True/false values (eligibility checks, status flags)



    * Add custom image and name for the requirement if you want
    * Click **"Add requirement"**\




Members connect their wallet and Guild automatically calls the specified contract method with the configured parameters. If the contract returns the expected output value, the member qualifies for the role.
