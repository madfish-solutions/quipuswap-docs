# 💾 Storage and types overview

### Storage

![](<../../../.gitbook/assets/image (6).png>)

### storage\_t

| Field              | Type                                                                                                        | Description                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| owner              | address                                                                                                     | Contract owner                                                              |
| ledger             | big\_map([ledger\_key\_t](storage-and-types-overview.md#ledger\_key\_t-is-tuple-address-nat), nat)          | User balance map                                                            |
| allowances         | big\_map([ledger\_key\_t](storage-and-types-overview.md#ledger\_key\_t-is-tuple-address-nat), set(address)) | A map of operators that are allowed to transfer tokens on behalf of a user. |
| collections        | big\_map(collection\_id\_t, collection\_t)                                                                  | Map of NFT collections                                                      |
| collection\_count  | nat                                                                                                         | Collections added counter                                                   |
| last\_minted_\__id | nat                                                                                                         | Identifier of the last NFT minted                                           |
| total\_supply      | nat                                                                                                         | Total number of all minted NFTs                                             |
| minters            | set(address)                                                                                                | Set of registered by owner minters                                          |
| metadata           | big\_map(string, bytes)                                                                                     | Smart contract metadata                                                     |
| token\_metadata    | big\_map(collection\_id\_t, token\_metadata\_t                                                              | Mapping of collection IDs to collection metadata                            |

### ledger\_key\_t is tuple(address \* nat)

| Type    | Description       |
| ------- | ----------------- |
| address | NFT owner address |
| nat     | nft id            |



### allowances\_t

#### Is big\_map([ledger\_key\_t,](storage-and-types-overview.md#ledger\_key\_t-is-tuple-address-nat) set(address))

| Field | Type                                                                       | Description                      |
| ----- | -------------------------------------------------------------------------- | -------------------------------- |
| key   | [ledger\_key\_t](storage-and-types-overview.md#ledger\_key\_t-address-nat) | NFT owner ledger key             |
|       |                                                                            |                                  |
| value | set(address)                                                               | Set of user's allowances for NFT |

### collection\_t

| Field              | Type | Description                           |
| ------------------ | ---- | ------------------------------------- |
| id                 | nat  | Collection ID                         |
| total\_supply      | nat  | Number of minted NFT Tokens           |
| max\_total\_supply | nat  | The maximum amount that can be minted |

###
