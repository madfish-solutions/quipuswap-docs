# vote

An entrypoint that executes [voting](../../../bucket-contract/entrypoints-overview/vote.md) for bakers on the specified [Bucket](../../../bucket-contract/) contract. Also, it updates users' global rewards and the rewards of the user who votes. Voting is possible only in TOK/TEZ liquidity pools (pairs).

### Call parameters

```pascaligo
type token_id_t         is nat

type dex_vote_t         is [@layout:comb] record [
  pair_id                 : token_id_t;
  candidate               : key_hash;
]
```

| Field     | Type               | Description                             |
| --------- | ------------------ | --------------------------------------- |
| pair\_id  | token\_id\_t (nat) | Identifier of the liquidity pool (pair) |
| candidate | key\_hash          | Baker the user votes for                |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    pair_id: 0,
    candidate: "tz1...",
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.vote(parmas).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `113` - a [Bucket](../../../bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `136` - reentrancy.
* `140` - can't perform voting because of zero LPs balance of the user.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
