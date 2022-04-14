# withdraw\_profit

An entrypoint that withdraws bakers' rewards from TOK/TEZ liquidity pools (pairs).

### Call parameters

```pascaligo
type token_id_t         is nat

type withdraw_profit_t  is [@layout:comb] record [
  receiver                : contract(unit);
  pair_id                 : token_id_t;
]
```

| Field    | Type           | Description                             |
| -------- | -------------- | --------------------------------------- |
| receiver | contract(unit) | Receiver of withdrawn bakers' rewards   |
| pair\_id | token\_id\_t   | Identifier of the liquidity pool (pair) |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    receiver: "tz1.../KT1...",
    pair_id: 0,
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.withdraw_profit(parmas).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `113` - a [Bucket](../../../bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `136` - reentrancy.
