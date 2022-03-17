# Guild API (Alpha)

### Role

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
         "value":"1",
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

{% tab title="Guild SDK" %}

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

{% tab title="Guild SDK" %}

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

{% tab title="Guild SDK" %}

{% endtab %}
{% endtabs %}

# Role Requirements



### COIN

```json
{
    "type": "COIN",
    "chain": string,     // supported chains: ETHEREUM, BSC, POLYGON, XDAI, FANTOM, AVALANCHE, ARBITRUM, HARMONY
    "data": {
        "amount": number // floating point number
    }
}
```

### ERC20 (TOKENS)

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

### ERC721 or ERC1155 (NFT)

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

```json
{
    "type": "POAP",
    "data": {
        "id": string // fancy_id of the POAP
    }
}
```

### [MIRROR](https://mirror.xyz)

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

### [SNAPSHOT](https://github.com/snapshot-labs/snapshot-strategies/tree/master/src/strategies)

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

### WHITELIST

```json
{
    "type": "WHITELIST",
    "data": {
        "addresses": string[] // the whitelisted user addresses
}
```

### FREE

```json
{
    "type": "FREE"
}
```


### Guild

{% swagger method="get" path="/guild" baseUrl="https://api.guild.xyz/v1" summary="Get all the existing guilds." %}
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

{% swagger method="get" path="/guild/:id" baseUrl="https://api.guild.xyz/v1" summary="Get a guild by id. Guild ID could be a number or an urlName of a guild." %}
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

{% swagger method="get" path="/guild/access/:id/:address" baseUrl="https://api.guild.xyz/v1" summary="Get User access to a Guild based on the Guild requirements." %}
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

{% swagger method="get" path="/guild/member/:id/:address" baseUrl="https://api.guild.xyz/v1" summary="Get User current accesses to a specific Guild." %}
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
// Code snippet
```
{% endtab %}
{% endtabs %}



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

{% tab title="Guild SDK" %}

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
{% endtab %}

{% tab title="Guild SDK" %}

{% endtab %}
{% endtabs %}


### User

{% swagger method="get" path="/user/membership/:address" baseUrl="https://api.guild.xyz/v1" summary="Get every membership of a User." %}
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

{% swagger method="post" path="/user/join" baseUrl="https://api.guild.xyz/v1" summary="Join user to a Guild" %}
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
