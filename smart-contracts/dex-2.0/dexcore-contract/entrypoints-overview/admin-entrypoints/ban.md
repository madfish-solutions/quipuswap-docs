# ban

An entrypoint that can ban or unban a baker on the specified [Bucket](../../../bucket-contract/) contract. Users can't vote for a baker who has been banned by an administrator.

### Call parameters

```pascaligo
type ban_baker_t        is [@layout:comb] record [
  baker                   : key_hash;
  ban_period              : nat;
]

type ban_t              is [@layout:comb] record [
  pair_id                 : token_id_t;
  ban_params              : ban_baker_t;
]
```

#### ban\_baker\_t

| Field       | Type      | Description                                                |
| ----------- | --------- | ---------------------------------------------------------- |
| baker       | key\_hash | A baker to ban or unban                                    |
| ban\_period | nat       | Period of banning (in seconds). Must be 0 to unban a baker |

#### ban\_t

| Field       | Type                                  | Description                         |
| ----------- | ------------------------------------- | ----------------------------------- |
| pair\_id    | token\_id\_t (nat)                    | Pool's ID where need to ban a baker |
| ban\_params | [ban\_baker\_t](ban.md#ban\_baker\_t) | Parameters of banning               |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    pair_id: 1,
    ban_params: {
        baker: "tz1...",
        ban_period: 60, // 1 minute
    },
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.ban(parmas).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `113` - a [Bucket](../../../bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `400` - `sender` of the transaction is not current administrator.
