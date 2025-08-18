# Custom API call

Check external APIs to verify member data or conditions not available on Guild. Perfect for integrating with custom databases, third-party services, or proprietary verification systems.

#### Setting up Custom API Call requirements:

* In the role editor, click **"Add requirements"** and select **Custom API Call**
* Enter the **URL** of your API endpoint, including any path and query parameters
* Use the literal template token `<ACCOUNT_ID>` anywhere you need to insert the user's wallet address:
  * Example: `https://my-api.com/wallets/<ACCOUNT_ID>/balance`
  * When verified: Guild replaces `<ACCOUNT_ID>` with the actual wallet address like `0x123..`
* If needed, add **Body of the request** - JSON data to send with your API call
* If needed, add **Headers of the request** - Custom headers like authentication tokens or content types
  * Click **"+ Add more"** to include multiple headers
* Select the **HTTP method** (GET, POST)
* Set the **Key** - Specify which field in the API response to check (e.g., `status`, `verified`, `balance`)
* Set the **Value** - Define what the response value should be (you can choose from equal, greater than, less than, etc.)
* Add custom image and name for the requirement if you want
* Click **"Add requirement"**

{% hint style="danger" %}
API calls made by Guild are public and can be reproduced by anyone with technical knowledge. Do not rely on this feature for sensitive data or assume the requests are private.
{% endhint %}

When members verify requirements, Guild calls your specified API endpoint and checks if the response contains the expected key-value pair. The member's wallet address is automatically inserted wherever you use `<ACCOUNT_ID>`.

Please ensure your API endpoint can handle Guild's verification requests and returns consistent JSON responses. Consider rate limiting and authentication for security.
