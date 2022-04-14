# check\_is\_banned\_baker

This on-chain view checks if baker on the specific [Bucket](../../bucket-contract/) contract is banned or not. If baker is banned, voting for him is not possible.

### Call parameters

```pascaligo
type token_id_t         is nat

type is_banned_baker_t  is key_hash

type check_is_banned_t  is [@layout:comb] record [
  pair_id                 : token_id_t;
  baker                   : is_banned_baker_t;
]
```

| Field    | Type                             | Description                                                   |
| -------- | -------------------------------- | ------------------------------------------------------------- |
| pair\_id | token\_id\_t (nat)               | Pair ID for which you need to check if baker is banned or not |
| baker    | is\_banned\_baker\_t (key\_hash) | Baker to check                                                |

### Return type

```pascaligo
bool
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = {
    pair_id: 1,
    baker: "tz1...",
};
const viewCaller = "tz1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const isBannedBaker = await dexCore.contract.contractViews.check_is_banned_baker(params).executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `113` - a [Bucket](../../bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `125` - [_**is\_banned\_baker**_](../../bucket-contract/on-chain-views-overview/is\_banned\_baker.md) view of [Bucket](../../bucket-contract/) contract isn't found.
