# update\_whitelist

An entrypoint that updates a list of whitelisted tokens. Tokens can be added to whitelist or can be removed from it.

Whitelisted tokens can be [withdrawn](withdraw\_public\_fee.md) by an administrator of the contract. Any user can [launch](../auction-entrypoints/launch\_auction.md) an auction for **NON** whitelisted tokens.

### Call parameters

```pascaligo
type tez_t              is unit

type fa12_token_t       is address

type fa2_token_t        is [@layout:comb] record [
  token                   : address;
  id                      : nat;
]

type token_t            is
| Tez                     of tez_t
| Fa12                    of fa12_token_t
| Fa2                     of fa2_token_t

type update_whitelist_t is [@layout:comb] record [
  token                   : token_t;
  add                     : bool;
]
```

| Field | Type     | Description                                         |
| ----- | -------- | --------------------------------------------------- |
| token | token\_t | FA1.2/FA2/TEZ token                                 |
| add   | bool     | Flag that indicates: admin adds a minter or removes |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const auctionAddress = "KT1...";
const params = {
    token: {
        token: "KT1...",
        id: 0,
    },
    add: true, // or false to remove from whitelist
};
const auction = await tezos.contract.at(auctionAddress);
const operation = await auction.methodsObject.update_whitelist(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
