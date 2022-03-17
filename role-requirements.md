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
