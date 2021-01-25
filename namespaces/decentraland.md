---
namespace: urn:decentraland
github-org: https://github.com/decentraland
contact-email: developers@decentraland.org
npm-package: "@dcl/urn-resolver"
---

# Description

Decentraland is a virtual reality platform powered by the Ethereum blockchain. 

# Resolver structure

The structure of the resolver is defined by a hierarchy of content address resolvers.

```yml
urn:decentraland:{protocol}:(...)
```

The hierarchy is defined by the `{protocol}` component of the URN.

## The Ethereum resolvers

Decentraland works in different blockchains and networks: There are 4 registered roots for blockchain assets:

- Ethereum Mainnet: `urn:decentraland:ethereum:{contract-or-alias}:{tokenId}`
- Ethereum Ropsten: `urn:decentraland:ropsten:{contract-or-alias}:{tokenId}`
- Ethereum Kovan: `urn:decentraland:kovan:{contract-or-alias}:{tokenId}`
- Ethereum Rinkeby: `urn:decentraland:rinkeby:{contract-or-alias}:{tokenId}`
- Ethereum Goerli: `urn:decentraland:goerli:{contract-or-alias}:{tokenId}`
- Matic Mainnet: `urn:decentraland:matic:{contract-or-alias}:{tokenId}`
- Matic Mumbai: `urn:decentraland:mumbai:{contract-or-alias}:{tokenId}`

### Aliases

For each protocol, to make the URN friendlyer to read, we specify some aliases, the aliases are defined in this live file: https://contracts.decentraland.org/addresses.json which should be used every time a contract needs to be resolved.

#### Example: Ethereum Mainnet

- `urn:decentraland:ethereum:LAND` resolves to `0xf87e31492faf9a91b02ee0deaad50d51d56d5d4d`
- `urn:decentraland:ethereum:ESTATE` resolves to `0x959e104E1a4dB6317fA58F8295F586e1A978c297`

Using that information, `urn:decentraland:ethereum:LAND:4763953136893138488487244504044754960247` resolves to `urn:decentraland:ethereum:0xf87e31492faf9a91b02ee0deaad50d51d56d5d4d:4763953136893138488487244504044754960247` which can be interpreted as:

```yml
# to validate ownership in the blochckain of urn:decentraland:ethereum:LAND:4763953136893138488487244504044754960247
blockchain: ethereum
network: mainnet
contractAddress: 0xf87e31492faf9a91b02ee0deaad50d51d56d5d4d (LAND)
id: 4763953136893138488487244504044754960247
```

### Content resolvers

Detailed URN resolution schemas are available at the repository [decentraland/urn-resolver](https://github.com/decentraland/urn-resolver/)

- `decentraland:off-chain:{registry}:{name}`: Resolve static offchain assets (i.e. base wearables, not in any blockchain nor content server)
- `decentraland:{protocol}:collections:v1:{contract(0x[a-fA-F0-9]+)}:{name}`: Resolve an ethereum wearables collection asset by contract address (v1)
- `decentraland:{protocol}:collections:v1:{collection-name}:{name}`: Resolve an ethereum wearables collection asset by collection name (wearables API) (v1)
- `decentraland:{protocol}:collections:v2:{contract(0x[a-fA-F0-9]+)}:{id}`: Resolve an ethereum wearables collection asset by contract address (v2)
- `decentraland:{protocol}:LAND:{x},{y}`: Resolves the ethereum asset of a LAND position.
- `decentraland:{protocol}:LAND:{tokenId}`: Resolves the ethereum asset of a LAND by tokenId.
- `decentraland:{protocol}:{contract(0x[a-fA-F0-9]+)}:{tokenId}`: Resolve an ethereum asset by contract address
- `decentraland:{protocol}:{contract([a-zA-Z][a-zA-Z_0-9]*)}:{tokenId}`: Resolve an ethereum asset by contract name

## Custom resolvers

For some use cases, like default wearables (non-blockchain based assets) we will use custom `off-chain` protocol.

This is so to avoid conflicts with future protocols and to easily differentiate blockchain assets from non-blockchain assets.

Following the pattern:  
`urn:decentraland:off-chain:{collection}:{assetId}`

We can get URNs like:  
`urn:decentraland:off-chain:base-avatars:top-hat-1`
