# MetaNet-Website
Demos and Instructions on How to Build a Website on BSV MetaNet.

## Get Started

1. Build a HTML page
2. upload it to bitcoin at b.bitdb.network

## Topic

### SiteLoader

Siteloader is kind of middleware that help browser access metanet website.

A website loader prepare pages, scripts and other resources from blockchain.

See [Siteloader](./SiteLoader)

For multi page website, see [metasite-loader](https://github.com/monkeylord/MetaSite-Loader)

### Data

See [Bitcoin Application Data protocol](https://github.com/monkeylord/BAD)

The basic principles are

1. Each data(Or data group) should have it's own key, we call it DataKey. 
2. From DataKey and other information, a deterministic cryptic prefix can be derived, which allow DataKey and only DataKey to search.
3. Data should be encrypted with key that derived deterministic from DataKey, which allow DataKey and only DataKey to decrypt.
4. Data should be signed with key derived deterministic from DataKey.

### User

In metanet, user is identity, which may be a master private key.

Neither the identity key nor its public key should exposed to public.

One should not use identity key to sign or transact.



All the other key are derived from identity key. 

The derivation path from identity key should be hardened to make sure identity key is not recoverable.

The derivation path from its child keys can be hardened (e.g DataKey)  or unhardened (e.g FilesystemKey).

Unhardened derivation allow deriving child public key from parent public key.

### Transaction

integrate Moneybutton in your html page.

implement a simple wallet whose xpriv is derived from identity key.

### Crypto

### Parameters

Parameters from `#`

### Security

### API and Protocol

## Advanced

### Chatroom

### Games on Chain

### News

### forum