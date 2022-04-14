# withdraw\_auction\_fee

An entrypoint that allows any user to withdraw an auction fee. Will withdraw all available fee. All fees will be transferred to the [Auction](../../../auction-contract/) contract and the sender of the transaction will receive a reward (% of the withdrawn amount) in tokens that were withdrawn.

### Call parameters

```pascaligo
type token_id_t         is nat

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

type withdraw_fee_t     is [@layout:comb] record [
  pair_id                 : option(token_id_t);
  token                   : token_t;
]
```

| Field    | Type                 | Description                             |
| -------- | -------------------- | --------------------------------------- |
| pair\_id | option(token\_id\_t) | Identifier of the liquidity pool (pair) |
| token    | token\_t             | FA1.2/FA2/TEZ token                     |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    pair_id: undefined, // or null, or an existing TOK/TEZ liquidity pool (pair) ID
    token: {
        fa2: {
            token: "KT1...",
            id: 0,
        },
    },
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.withdraw_auction_fee(parmas).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `136` - reentrancy.
* `143` - `pair_id` parameter not provided (in case of withdrawing TEZ tokens).&#x20;
