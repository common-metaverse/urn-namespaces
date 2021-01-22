# A common identifier for assets across the metaverse projects

Identifying a blockchain asset is difficult. Wallets, exchanges, tools and other pieces of software need to know the specifics about how to interact with the project's infrastructure to get images or to render content. This repository aims to resolve the content addressing mechanisms to embed our crypto-art, assets, wearables and avatars into different metaverse projects using a common identifier.

## URN

A Uniform Resource Name ([URNs](https://en.wikipedia.org/wiki/Uniform_Resource_Name)) are globally unique persistent identifiers assigned within defined namespaces so they will be available for a long period of time, even after the resource which they identify ceases to exist or becomes unavailable.

# Registered namespaces

- `urn:cryptovoxels` - https://www.cryptovoxels.com - [Namespace documentation](namespaces/cryptovoxels.md)
- `urn:decentraland` - https://decentraland.org - [Namespace documentation](namespaces/decentraland.md)
- `urn:thesandboxgame` - https://www.sandbox.game - [Namespace documentation](namespaces/thesandboxgame.md)

# Adding a namespace

1. Fork this project
2. Set the name of your namespace (equals to the Github organization name)
3. Create a `namespaces/{your-namespace}.md` file
4. Add the file to README.md (ordered alphabetically)
5. Send a pull request. We will wait for someone in the organization (same as namespace) to come along and approve the pull request. To avoid ownership problems, only organizations with verified domains will be accepted, that way, we are delegating ownership validation to Github.

# Rationale

URN are composed of three main elements: Header (`urn:`), A namespace, and an NSS (namespace-specific string) forming a string in the shape `urn:{namespace}:{nss}`.  

The proposal only enforces that the namespace is part of a well-known list of namespaces with mappings to APIs or docummentation on how to resolve the NSS part of the asset.  

I.e, in Decentraland, they are using the format `urn:decentraland:{chain-identifier}:{contract}:{tokenid}` to identify every asset.  

Some examples of this implementation could be:

```yml
urn:cryptovoxels:ethereum:COLR:0x1
urn:decentraland:matic:0x000000000123123:0x332
urn:thesandboxgame:ethereum:LAND:0x1010
urn:decentraland:matic:quests:1
```

## Extensibility

After the namespace-specific string, a query string component is a valid part of any URN, making extensions not only possible but very easy to parse and implement. 

```yml
urn:decentraland:ethereum:LAND:0x1010?atBlock=1231411231
```

## Benefit

* Wallets and service providers like exchanges could start indexing assets unequivocally using a common ID.
* By documenting namespaces and its content resolution, tool developers would have a lower entry barrier fostering innovation of the ecosystem and the rise of the metaverse.
* Take an initial step to portability and interoperability of assets across the metaverse.
* URN are designed to last forever. Completely decoupled from absolute URLs and servers.

## Summarizing
- Identify assets using `urn:{metaverse-namespace}:{custom-string}`.  
- `{custom-string}` is a namespace-specific string, hierarchically separating the parts of the custom-string with colon `:` is recommended and friendlyer than `/` for URL encoding (`urn:decentraland:ethereum:LAND:0x1` instead of `urn:decentraland:ethereum/LAND/0x1`).  
