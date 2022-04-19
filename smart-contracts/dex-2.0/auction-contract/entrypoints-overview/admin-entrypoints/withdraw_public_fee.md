# withdraw\_public\_fee

An entrypoint that allows the administrator of the contract to withdraw public fee that was accrued during the input of tokens to the this contract from [DexCore](../../../dexcore-contract/) contract (see [_**withdraw\_auction\_fee**_](../../../dexcore-contract/entrypoints-overview/dex-entrypoints/withdraw\_auction\_fee.md) entrypoint).

{% hint style="danger" %}
Only whitelisted tokens can be withdrawn (see [_**update\_whitelist**_](update\_whitelist.md) entrypoint).
{% endhint %}

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

type withdraw_fee_t     is [@layout:comb] record [
  token                   : token_t;
  receiver                : address;
]
```

| Field    | Type     | Description                  |
| -------- | -------- | ---------------------------- |
| token    | token\_t | FA1.2/FA2/TEZ token          |
| receiver | address  | Receiver of withdrawn tokens |

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
    receiver: "KT1.../tz1...",
};
const auction = await tezos.contract.at(auctionAddress);
const operation = await auction.methodsObject.withdraw_public_fee(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `306` - token for withdrawing is NOT whitelisted.
* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
