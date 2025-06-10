---
description: API for automating token gated access in any applications.
---

# Guild for Developers

_Check out our SDK here:_  [_https://www.npmjs.com/package/@guildxyz/sdk_](https://www.npmjs.com/package/@guildxyz/sdk)&#x20;

## Guilds

## Create Guild

<mark style="color:green;">`POST`</mark> `https://api.guild.xyz/v1/guild`

#### Request Body

| Name                                         | Type   | Description |
| -------------------------------------------- | ------ | ----------- |
| payload<mark style="color:red;">\*</mark>    | Object |             |
| validation<mark style="color:red;">\*</mark> | Object |             |

{% tabs %}
{% tab title="201: Created created guild" %}
```json
{
   "id":2244,
   "name":"api-test",
   "urlName":"api-test",
   "description":"",
   "imageUrl":"/guildLogos/145.svg",
   "createdAt":"2022-03-09T17:28:52.153Z",
   "showMembers":true
}
```
{% endtab %}

{% tab title="400: Bad Request errors occurred" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}

{% tab title="401: Unauthorized authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

Guild is an atomic unit of every communities

{% tabs %}
{% tab title="Guild SDK" %}
```typescript
import { guild, user } from "@guildxyz/sdk";
import { ethers } from "ethers";



// Creating a random wallet for the example
const wallet = ethers.Wallet.createRandom();
// Wrapping the signer function from ethers.js
const sign = (signableMessage: string | Bytes) =>
  ethersWallet.signMessage(signableMessage);

// Creating a Guild
const myGuild = await guild.create(
  wallet.address, // You have to insert your own wallet here
  sign,
  {
    name: "My New Guild",
    description: "Cool stuff", // Optional
    imageUrl: "", // Optional
    theme: [{ mode: "DARK", color: "#000000" }], // Optional
    roles: [
      {
        name: "My First Role",
        logic: "AND",
        requirements: [
          {
            type: "ALLOWLIST",
            data: {
              addresses: [
                "0xedd9C1954c77beDD8A2a524981e1ea08C7E484Be",
                "0x1b64230Ad5092A4ABeecE1a50Dc7e9e0F0280304",
              ],
            },
          },
        ],
      },
      {
        name: "My Second Role",
        logic: "OR",
        requirements: [
          {
            type: "ERC20",
            chain: "ETHEREUM",
            address: "0xf76d80200226ac250665139b9e435617e4ba55f9",
            data: {
              amount: 1,
            },
          },
          {
            type: "ERC721",
            chain: "ETHEREUM",
            address: "0x734AA2dac868218D2A5F9757f16f6f881265441C",
            data: {
              amount: 1,
            },
          },
        ],
      },
    ],
  }
);
```
{% endtab %}

{% tab title="API" %}
```json
{
   "payload":{
      "name": string,
      "imageUrl"?: string,
      "description"?: string,
      "roles": Role[],
      "theme"?: Theme[],
      "showMembers"?: boolean
   },
   "validation": {
      // Validation object
   }
}
```
{% endtab %}
{% endtabs %}

## Get All Guilds

<mark style="color:blue;">`GET`</mark> `https://api.guild.xyz/v1/guild`

{% tabs %}
{% tab title="200: OK array of guilds" %}
```json
[
    {
        "id": number,
        "name": string,
        "roles": string[], // names of the roles
        "imageUrl": string,
        "urlName": string,
        "memberCount": number
    }
]
```
{% endtab %}

{% tab title="204: No Content empty response, not found" %}
**No Guild added.**
{% endtab %}
{% endtabs %}

## Check User Access to a Guild

<mark style="color:blue;">`GET`</mark> `https://api.guild.xyz/v1/guild/access/:id/:address`

The response is separated by role identifiers.

#### Path Parameters

| Name                                      | Type   | Description         |
| ----------------------------------------- | ------ | ------------------- |
| id<mark style="color:red;">\*</mark>      | number | id of the guild     |
| address<mark style="color:red;">\*</mark> | string | address of the user |

{% tabs %}
{% tab title="200: OK array of accesses" %}
```json
[
   {
      "roleId":2339,
      "access":true
   },
   {
      "roleId":2015,
      "access":true
   },
   {
      "roleId":99,
      "access":false
   }
]
```
{% endtab %}

{% tab title="400: Bad Request errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}

{% tab title="500: Internal Server Error errors occurred, but response still available" %}
```json
[
   {
      "roleId":2540,
      "access":true
   },
   {
      "roleId":2560,
      "access":null,
      "errors":[
         {
            "requirementId":5861,
            "msg":"Multicall received an empty response. Check your call configuration for errors."
         }
      ]
   },
   {
      "roleId":2537,
      "access":false
   },
   {
      "roleId":2538,
      "access":false
   }
]
```
{% endtab %}
{% endtabs %}

## Get User

<mark style="color:blue;">`GET`</mark> `https://api.guild.xyz/v1/guild/member/:id/:address`

#### Path Parameters

| Name                                      | Type   | Description         |
| ----------------------------------------- | ------ | ------------------- |
| id<mark style="color:red;">\*</mark>      | number | id of the guild     |
| address<mark style="color:red;">\*</mark> | string | address of the user |

{% tabs %}
{% tab title="200: OK " %}
```json
   [
      {
         "roleId":1034,
         "access":false
      },
      {
         "roleId":1031,
         "access":false
      },
      {
         "roleId":1175,
         "access":true
      }
   ]
```
{% endtab %}

{% tab title="400: Bad Request errors occurred" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Get Guilds Joined by a User

<mark style="color:blue;">`GET`</mark> `https://api.guild.xyz/v1/user/membership/:address`

#### Path Parameters

| Name                                      | Type   | Description         |
| ----------------------------------------- | ------ | ------------------- |
| address<mark style="color:red;">\*</mark> | string | address of the user |

{% tabs %}
{% tab title="200: OK " %}
```javascript
[
   {
      "guildId":13,
      "roleids":[
         397
      ]
   },
   {
      "guildId":21,
      "roleids":[
         1175
      ]
   },
   {
      "guildId":1533,
      "roleids":[
         2339,
         2015
      ]
   },
]
```
{% endtab %}

{% tab title="400: Bad Request errors occurred" %}
```javascript
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Join a Guild

<mark style="color:green;">`POST`</mark> `https://api.guild.xyz/v1/user/join`

#### Request Body

| Name                                         | Type   | Description |
| -------------------------------------------- | ------ | ----------- |
| payload<mark style="color:red;">\*</mark>    | Object |             |
| validation<mark style="color:red;">\*</mark> | Object |             |

{% tabs %}
{% tab title="200: OK " %}
```javascript
[

]
```
{% endtab %}

{% tab title="400: Bad Request errors occurred" %}
```javascript
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}

{% tab title="401: Unauthorized authentication required" %}
```javascript
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Guild SDK" %}
```typescript
import { user } from "@guildxyz/sdk";
import { ethers } from "ethers";

// Joining to a Guild if any role is accessible by the given address
await user.join(
    guildId,                        // Insert Guild ID here
    walletAddress,                  // Your wallet address
    signerFunction);                // Your lib's signing method
```
{% endtab %}

{% tab title="API" %}
```json
{
      "payload": {
            "guildId": number
      },
      "validation": {
      // Validation object
      }
}
```
{% endtab %}
{% endtabs %}

## Get a Guild by ID

<mark style="color:blue;">`GET`</mark> `https://api.guild.xyz/v1/guild/:id`

#### Path Parameters

| Name                                 | Type   | Description             |
| ------------------------------------ | ------ | ----------------------- |
| id<mark style="color:red;">\*</mark> | string | id/urlName of the guild |

{% tabs %}
{% tab title="200: OK guild object" %}
```json
{
    "id": number,
    "name": string,
    "urlName": string,
    "description": string,
    "imageUrl": string,
    "showMembers": boolean,
    "admins": [
        {
            "id": number,
            "address": string,
            "isOwner": boolean
        },
    ],
    "theme": {
            "mode": "DARK" | "LIGHT",
            "color": string,
            "backgroundCss": string,
            "backgroundImage": string
    },
    "platforms": [
        {
            "id": number,
            "platformId": string,
            "type": "DISCORD" | "TELEGRAM",
            "platformName": string,
        }
    ],
    "roles": [
                {
                    "id": number,
                    "name": string,
                    "description": string,
                    "imageUrl": string,
                    "logic": "AND" | "OR" | "NAND" | "NOR",
                    "requirements": Requirement[],
                    "members": string[], // array of addresses
                    "memberCoun": number,
                
                }
    ]       
}
```
{% endtab %}

{% tab title="204: No Content empty response, not found" %}
**Specified Guild doesn't exist with the given ID or urlName.**
{% endtab %}
{% endtabs %}

Guild ID could be a number or an urlName of a guild.

## Update Guild

<mark style="color:purple;">`PATCH`</mark> `https://api.guild.xyz/v1/guild/:id`

#### Request Body

| Name                                         | Type   | Description |
| -------------------------------------------- | ------ | ----------- |
| payload<mark style="color:red;">\*</mark>    | Object |             |
| validation<mark style="color:red;">\*</mark> | Object |             |

{% tabs %}
{% tab title="200: OK array of accesses to roles" %}
```json
///
```
{% endtab %}

{% tab title="400: Bad Request errors occurred" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}

{% tab title="401: Unauthorized authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

**Automate new role creation, manage hundreds of roles and update them on the fly.**

A few examples where this could be useful:

1. Extend an allow list automatically.
2. Users can invite others by adding their address to an allow list.

{% tabs %}
{% tab title="Guild SDK" %}
```typescript
import { guild } from "@guildxyz/sdk";
import { ethers } from "ethers";
    
await guild.update(
        guildId,                     // Insert Guild ID here
        walletAddress,               // Your wallet address
        signerFunction,              // Your lib's signing method
        updateGuildParams);          // Params
```
{% endtab %}

{% tab title="API" %}
```json
{
   "payload":{
      "name": string,
      "imageUrl": string,
      "description": string,
      "roles": Role[],
      "theme": Theme[],
      "showMembers": boolean
   },
   "validation": {
        // Validation object
   }
}
```
{% endtab %}
{% endtabs %}

## Delete Guild

<mark style="color:red;">`DELETE`</mark> `https://api.guild.xyz/v1/guild/:id`

#### Path Parameters

| Name                               | Type   | Description |
| ---------------------------------- | ------ | ----------- |
| <mark style="color:red;">\*</mark> | number |             |

#### Request Body

| Name                                         | Type   | Description |
| -------------------------------------------- | ------ | ----------- |
| payload<mark style="color:red;">\*</mark>    | Object |             |
| validation<mark style="color:red;">\*</mark> | Object |             |

{% tabs %}
{% tab title="200: OK " %}
```json
{
    "success": boolean
}
```
{% endtab %}

{% tab title="400: Bad Request errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}

{% tab title="401: Unauthorized authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Guild SDK" %}
```typescript
import { guild } from "@guildxyz/sdk";
import { ethers } from "ethers";

await guild.delete(
        guildId,                     // Insert Guild ID here
        walletAddress,               // Your wallet address
        signerFunction);             // Your lib's signing method
```
{% endtab %}

{% tab title="API" %}
```json
{
   "payload":{
      // Empty object is necessary
   },
   "validation": {
      // Validation object
   }
}
```
{% endtab %}
{% endtabs %}

## Roles

## Get Role

<mark style="color:blue;">`GET`</mark> `https://api.guild.xyz/v1/role/:id`

#### Path Parameters

| Name                               | Type   | Description |
| ---------------------------------- | ------ | ----------- |
| <mark style="color:red;">\*</mark> | number |             |

{% tabs %}
{% tab title="200: OK " %}
```json
{
   "imageUrl":"/guildLogos/107.svg",
   "name":"Member",
   "description":"",
   "logic":"AND",
   "requirements":[
      {
         "type":"ERC20",
         "address":"0x1b6c5864375b34af3ff5bd2e5f40bc425b4a8d79",
         "alue":"1",
         "chain":"ETHEREUM"
      }
   ],
   }
```
{% endtab %}

{% tab title="204: No Content " %}
**Specified Role doesn't exist with the given ID.**
{% endtab %}
{% endtabs %}

Roles are the building-blocks of all guilds. You can create as many as you want to distinguish users by certain conditions.

Each role can represent a membership type, grant temporary or permanent access to content in your application.

Common use-cases include:

1. **Membership tiers**
2. **Clubs**
3. **Permission management for work collaboration.**
4. **Access** to articles.
5. **Ticket** to a virtual event or IRL.
6. **Special privileges** in a social application.

## Create Role

<mark style="color:green;">`POST`</mark> `https://api.guild.xyz/v1/role`

#### Request Body

| Name                                         | Type   | Description |
| -------------------------------------------- | ------ | ----------- |
| payload<mark style="color:red;">\*</mark>    | Object |             |
| validation<mark style="color:red;">\*</mark> | Object |             |

{% tabs %}
{% tab title="201: Created Created Role" %}
```json
{
   "imageUrl":"/guildLogos/107.svg",
   "name":"Member",
   "description":"",
   "logic":"AND",
   "requirements":[
      {
         "type":"ERC20",
         "address":"0x1b6c5864375b34af3ff5bd2e5f40bc425b4a8d79",
         "value":"1",
         "chain":"ETHEREUM"
      }
   ]
}
```
{% endtab %}

{% tab title="400: Bad Request errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}

{% tab title="401: Unauthorized authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

To create a new role, you need to define its requirements and the logic type of stacking these requirements.

{% tabs %}
{% tab title="Guild SDK" %}
```typescript
import { role } from "@guildxyz/sdk";
import { ethers } from "ethers";

await role.create(
      walletAddress,                 // Your wallet address
      signerFunction,                // Your lib's signing method
      {
        guildId: 1,                  // Insert Guild ID here
        name: "My Third Role",
        logic: "AND",
        requirements: [
          {
            type: "ALLOWLIST",
            data: {
              addresses: [
                "0xedd9C1954c77beDD8A2a524981e1ea08C7E484Be",
              ],
            },
          },
        ],
      });

```
{% endtab %}

{% tab title="API" %}
```json
{
   "payload":{
      "name": string,
      "imageUrl"?: string,
      "description"?: string,
      "logic": "AND" | "OR" | "NAND" | "NOR",
      "requirements": Requirement[]
   },
   "validation": {
      // Validation object
   }
}
```
{% endtab %}
{% endtabs %}

## Update Role

<mark style="color:purple;">`PATCH`</mark> `https://api.guild.xyz/v1/role/:id`

#### Path Parameters

| Name                               | Type   | Description |
| ---------------------------------- | ------ | ----------- |
| <mark style="color:red;">\*</mark> | number |             |

#### Request Body

| Name                                         | Type   | Description |
| -------------------------------------------- | ------ | ----------- |
| payload<mark style="color:red;">\*</mark>    | Object |             |
| validation<mark style="color:red;">\*</mark> | Object |             |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="400: Bad Request errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}

{% tab title="401: Unauthorized authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

You can update roles anytime, but be aware that existing members might loose access to their guild if the requirements change.

Updating roles programatically is a powerful way to manage communities with dynamic membership requirements or keep requirements up-to-date automatically.

{% tabs %}
{% tab title="Guild SDK" %}
```typescript
import { role } from "@guildxyz/sdk";
import { ethers } from "ethers";

await role.update(
        roleId,                      // Insert Role ID here
        walletAddress,               // Your wallet address
        signerFunction,              // Your lib's signing method
        updateGuildParams);          // Params
```
{% endtab %}

{% tab title="API" %}
```json
{
   "payload":{
      "name": string,
      "imageUrl": string,
      "description": string,
      "logic":"AND" | "OR" | "NAND" | "NOR",
      "requirements": Requirement[]
   },
   "validation": {
      // Validation object
   }
}
```
{% endtab %}
{% endtabs %}

## Delete Role

<mark style="color:red;">`DELETE`</mark> `https://api.guild.xyz/v1/role/:id`

#### Path Parameters

| Name                               | Type   | Description |
| ---------------------------------- | ------ | ----------- |
| <mark style="color:red;">\*</mark> | number |             |

#### Request Body

| Name                                         | Type   | Description |
| -------------------------------------------- | ------ | ----------- |
| payload<mark style="color:red;">\*</mark>    | Object |             |
| validation<mark style="color:red;">\*</mark> | Object |             |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    "success": boolean
}
```
{% endtab %}

{% tab title="400: Bad Request errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}

{% tab title="401: Unauthorized authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Guild SDK" %}
```typescript
import { role } from "@guildxyz/sdk";
import { ethers } from "ethers";

await role.delete(
        guildId,                     // Insert Guild ID here
        walletAddress,               // Your wallet address
        signerFunction);             // Your lib's signing method
```
{% endtab %}

{% tab title="API" %}
```json
{
   "payload":{
      // Empty object is necessary
   },
   "validation": {
      // Validation object
   }
}
```
{% endtab %}
{% endtabs %}

## Requirements

Guild enables requirement creation based on standard contract types and integrated protocols.

### COIN

Native fungible tokens of supported blockchains.

```json
{
    "type": "COIN",
    "chain": string,     // supported chains: ETHEREUM, BSC, POLYGON, XDAI, FANTOM, AVALANCHE, ARBITRUM, HARMONY
    "data": {
        "amount": number // floating point number
    }
}
```

### ERC-20

Commonly referred to as tokens.

```json
{
    "type": "ERC20",
    "chain": string,     // supported chains: ETHEREUM, BSC, POLYGON, XDAI, FANTOM, AVALANCHE, ARBITRUM, HARMONY
    "address": string,   // contract address
    "data": {
        "amount": number // floating point number
    }
}
```

### ERC-721 or ERC-1155

Commonly referred to as NFTs.

```json
{
    "type": "ERC721" | "ERC1155",
    "chain": string,      // supported chains: ETHEREUM, BSC, POLYGON, XDAI, FANTOM, AVALANCHE, ARBITRUM, HARMONY
    "address": string,    // contract address
    "data": {
        "id": number,     // tokenId (optional)
        "amount": number, // integer, number of NFTs to hold,
        "attribute": {    // required attribute of the NFT (optional)
            "trait_type": string,              // key of the attribute
            "value": string // value of the attribute
            "interval": {"min": number, "max": number} // interval of the attribute
        }
    }
}
```

### [POAP](https://poap.xyz)

NFTs issued by the Proof of Attendance Protocol (POAP) represent special shared memories.

```json
{
    "type": "POAP",
    "data": {
        "id": string // fancy_id of the POAP
    }
}
```

### [MIRROR](https://mirror.xyz)

NFTs minted on Mirror.xyz, the web3-native publishing platform.

```json
{
    "type": "MIRROR",
    "chain": string,   // supported chains: ETHEREUM, BSC, POLYGON, XDAI, FANTOM, AVALANCHE, ARBITRUM, HARMONY
    "address": string, // constract address
    "data": {
        "id": number   // ediotion id, TODO: how do we know the edition number
    }
}
```

### [UNLOCK](https://unlock-protocol.com)

Membership NFTs issued by the Unlock Protocol.

```json
{
    "type": "UNLOCK",
    "chain": string,   // supported chains: ETHEREUM, BSC, POLYGON, XDAI
    "address": string, // contract address
    "data": {
        "amount": number
    }
}
```

### [SNAPSHOT](https://github.com/snapshot-labs/snapshot-strategies/tree/master/src/strategies) STRATEGIES

Snapshot strategies are JavaScript functions that return a score for a set of addresses. They are being used on Guild to enable any custom condition check.

Currently available strategies: [https://github.com/snapshot-labs/snapshot-strategies/tree/master/src/strategies](https://github.com/snapshot-labs/snapshot-strategies/tree/master/src/strategies)

Learn how to create a new strategy: [https://docs.snapshot.org/strategies/create](https://docs.snapshot.org/strategies/create)

```json
{
    "type": "SNAPSHOT",
    "chain": string,       // supported chains: ETHEREUM, BSC, POLYGON, XDAI, FANTOM, AVALANCHE, ARBITRUM, HARMONY
    "data": {
        "startegy": object // strategy object, e.g. in https://github.com/snapshot-labs/snapshot-strategies/blob/master/src/strategies/aave-governance-power/examples.json 
    }
}
```

### [JUICEBOX](https://juicebox.money/#/)

Tokens created with Juicebox protocol, so communities can utilize their tokens while they are still staked.

```json
{
    "type": "JUICEBOX",
    "chain": string,     // supported chains: ETHEREUM, BSC, POLYGON, XDAI, FANTOM, AVALANCHE, ARBITRUM, HARMONY
    "data": {
        "id": number,    // id of the project,
        "amount": number // minimum amount staked
    }
}
```

### ALLOWLIST

Allow lists, commonly referred to as "whitelists" enable curation based on a list of wallet addresses collected from an external source.

```json
{
    "type": "ALLOWLIST",
    "data": {
        "addresses": string[] // the allowed user addresses
    }
}
```

### FREE

Guest pass for guild members without any requirements.

```json
{
    "type": "FREE"
}
```
