# claim\_interface\_fee

An entrypoint that allows users to claim their interface (referral) fee. Will claim all available fee. Supports only withdrawing of FA1.2 or FA2 tokens. To withdraw TEZ tokens use [_**claim\_interface\_tez\_fee**_](claim\_interface\_tez\_fee.md) entrypoint.

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

type claim_fee_t        is [@layout:comb] record [
  token                   : token_t;
  receiver                : address;
]
```

| Field    | Type     | Description                  |
| -------- | -------- | ---------------------------- |
| token    | token\_t | FA1.2/FA2 token              |
| receiver | address  | Receiver of withdrawn tokens |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    token: {
        fa2: {
            token: "KT1...",
            id: 0,
        },
    },
    receiver: "tz1.../KT1...",
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.claim_interface_fee(parmas).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `136` - reentrancy.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
