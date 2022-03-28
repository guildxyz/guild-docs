---
description: API for automating token gated access in any applications.
---

# Guild API (Alpha)

#### Guild.xyz is the membership layer protocol for web3 communities, making community management easy and interoperable between platforms.

## Guilds

_"Although there is no one single definition for what a web3 guild is, they’re generally considered to be a collective of crypto-enabled developers, designers, and thinkers that share resources (be it knowledge or labour) in the pursuit of a common goal." (_[_Web3 Guilds_](https://medium.com/superfluid-blog/web3-guilds-the-rebirth-of-organized-work-e9c1a139ad29)_)_

{% swagger method="post" path="/guild" baseUrl="https://api.guild.xyz/v1" summary="Create Guild" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="payload" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="validation" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="201: Created" description="created guild" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occurred" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

Create a new community by creating a guild.

{% tabs %}
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

{% tab title="Guild SDK" %}
```typescript
import { guild } from "@guildxyz/sdk";
import { ethers } from "ethers";
await guild.create(
  {
    name: "My New Guild",
    description: "Cool stuff",                                                      // Optional
    imageUrl: "",                                                                   // Optional
    theme: [{ mode: "DARK", color: "#000000" }],                                    // Optional
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
              amount: 1 
          },
          },
          {
            type: "ERC721",
            chain: "ETHEREUM",
            address: "0x734AA2dac868218D2A5F9757f16f6f881265441C",
            data: {
              amount: 1
            },
          },
        ],
      },
    ],
  },
  ethers.Wallet.createRandom() // You have to insert your own wallet here
);// Code snippet
```
{% endtab %}
{% endtabs %}

{% swagger method="get" path="/guild" baseUrl="https://api.guild.xyz/v1" summary="Get All Guilds" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="array of guilds" %}
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
{% endswagger-response %}

{% swagger-response status="204: No Content" description="empty response, not found" %}
**No Guild added.**
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/guild/access/:id/:address" baseUrl="https://api.guild.xyz/v1" summary="Check User Access to a Guild" %}
{% swagger-description %}
The response is separated by role identifiers.
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="number" required="true" %}
id of the guild
{% endswagger-parameter %}

{% swagger-parameter in="path" name="address" type="string" required="true" %}
address of the user
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="array of accesses" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="errors occurred, but response still available" %}
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
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/guild/member/:id/:address" baseUrl="https://api.guild.xyz/v1" summary="Get User's Membership Status in a Guild" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="number" required="true" %}
id of the guild
{% endswagger-parameter %}

{% swagger-parameter in="path" name="address" type="string" required="true" %}
address of the user
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occurred" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/user/membership/:address" baseUrl="https://api.guild.xyz/v1" summary="Get Guilds Joined by a User" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="address" type="string" required="true" %}
address of the user
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occurred" %}
```javascript
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/user/join" baseUrl="https://api.guild.xyz/v1" summary="Join a Guild" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="payload" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="validation" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
[

]
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occurred" %}
```javascript
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="authentication required" %}
```javascript
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
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

{% tab title="Guild SDK" %}
```typescript
???

// Installation: https://github.com/alchemyplatform/alchemy-web3

import { createAlchemyWeb3 } from "@alch/alchemy-web3";

// Using HTTPS
const web3 = createAlchemyWeb3(
  "https://eth-mainnet.alchemyapi.io/v2/demo",
);

const nfts = await web3.alchemy.getNfts({owner: "0xC33881b8FD07d71098b440fA8A3797886D831061"})

{
    payload: {
        guildId: 2124
    }
    validation
}{
```
{% endtab %}
{% endtabs %}

{% swagger method="get" path="/guild/:id" baseUrl="https://api.guild.xyz/v1" summary="Get a Guild by ID" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" required="true" %}
id/urlName of the guild
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="guild object" %}
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
{% endswagger-response %}

{% swagger-response status="204: No Content" description="empty response, not found" %}
**Specified Guild doesn't exist with the given ID or urlName.**
{% endswagger-response %}
{% endswagger %}

Guild ID could be a number or an urlName of a guild.

{% swagger method="patch" path="/guild/:id" baseUrl="https://api.guild.xyz/v1" summary="Update Guild" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="payload" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="validation" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="array of accesses to roles" %}
```json
///
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occurred" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
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

{% swagger method="delete" path="/guild/:id" baseUrl="https://api.guild.xyz/v1" summary="Delete Guild" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" type="number" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="payload" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="validation" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```json
{
    "success": boolean
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
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

## Roles

{% swagger method="get" path="/role/:id" baseUrl="https://api.guild.xyz/v1" summary="Get Role" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" type="number" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
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
{% endswagger-response %}

{% swagger-response status="204: No Content" description="" %}
**Specified Role doesn't exist with the given ID.**
{% endswagger-response %}
{% endswagger %}

Roles are the building-blocks of all guilds. You can create as many as you want to distinguish users by certain conditions.

Each role can represent a membership type, grant temporary or permanent access to content in your application.

Common use-cases include:

1. &#x20;Permission management for work collaboration.
2. Membership access to articles or newsletter.
3. Ticket to a virtual event.
4. Special privileges in a social application.

Besides integrating Guild into new platforms, this API is also useful for communities that need more control over their membership layers. You can **automate new role creation, manage hundreds of roles and update roles on the fly.**

A few examples where this could be useful:

1. An NFT issuer platform can create new roles for every new collection.
2. Extend an allow list automatically.
3. Users can invite others by adding their address to an allow list.

{% swagger method="post" path="/role" baseUrl="https://api.guild.xyz/v1" summary="Create Role" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="payload" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="validation" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="201: Created" description="Created Role" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

To create a new role, you need to define its requirements and the logic type of stacking these requirements.

{% tabs %}
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

{% swagger method="patch" path="/role/:id" baseUrl="https://api.guild.xyz/v1" summary="Update Role" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" type="number" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="payload" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="validation" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

You can update roles anytime, but be aware that existing members might loose access to their guild if the requirements change.

Updating roles programatically is a powerful way to manage communities with dynamic membership requirements or keep requirements up-to-date automatically.

{% tabs %}
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

{% swagger method="delete" path="/role/:id" baseUrl="https://api.guild.xyz/v1" summary="Delete Role" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" type="number" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="payload" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="validation" type="Object" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "success": boolean
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="errors occured" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="authentication required" %}
```json
{
    "errors": [
        {
            "msg": string
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
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
```

### FREE

Guest pass for guild members without any requirements.

```json
{
    "type": "FREE"
}
```

{% endtab %}
{% endtabs %}
