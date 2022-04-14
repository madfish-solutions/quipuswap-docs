# claim\_interface\_tez\_fee

An entrypoint that allows users to claim their interface (referral) fee. Will claim all available fee. Supports only withdrawing of TEZ tokens from the specific [Bucket](../../../bucket-contract/) contract. To withdraw TEZ tokens use [_**claim\_interface\_fee**_](claim\_interface\_fee.md) entrypoint.

### Call parameters

```pascaligo
type token_id_t         is nat

type claim_tez_fee_t    is [@layout:comb] record [
  pair_id                 : token_id_t;
  receiver                : address;
]
```

| Field    | Type               | Description                             |
| -------- | ------------------ | --------------------------------------- |
| pair\_id | token\_id\_t (nat) | Identifier of the liquidity pool (pair) |
| receiver | address            | Receiver of withdrawn tokens            |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    pair_id: 0,
    receiver: "tz1.../KT1...",
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.claim_interface_tez_fee(parmas).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `113` - a [Bucket](../../../bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `136` - reentrancy.
* `409` - TEZ tokens receiver contract not found (not user account or contract doesn't have a `default` entrypoint).
