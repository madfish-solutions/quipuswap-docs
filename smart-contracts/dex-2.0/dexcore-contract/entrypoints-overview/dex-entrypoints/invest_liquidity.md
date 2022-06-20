# invest\_liquidity

An entrypoint for liquidity investment in the specific liquidity pool (pair). Also it [votes](../../../bucket-contract/entrypoints-overview/vote.md) for the users' bakers in case of liquidity investment to TOK/TEZ pools.

### Call parameters

```pascaligo
type token_id_t         is nat

type invest_liquidity_t is [@layout:comb] record [
  pair_id                 : token_id_t;
  token_a_in              : nat;
  token_b_in              : nat;
  shares                  : nat;
  shares_receiver         : address;
  candidate               : key_hash;
  deadline                : timestamp;
]
```

| Field            | Type               | Description                                                                 |
| ---------------- | ------------------ | --------------------------------------------------------------------------- |
| pair\_id         | token\_id\_t (nat) | Identifier of the liquidity pool (pair)                                     |
| token\_a\_in     | nat                | Max amount of token A allowed to be spent                                   |
| token\_b\_in     | nat                | Max amount of token B allowed to be spent                                   |
| shares           | nat                | Amount of LP tokens to be acquired                                          |
| shares\_receiver | address            | Receiver of LP tokens                                                       |
| candidate        | key\_hash          | Baker for voting (is used only in time of investment to TOK/TEZ exchanges)  |
| deadline         | timestamp          | The time until which the transaction remains valid and will not be rejected |

### Usage

{% hint style="danger" %}
Note: you need to pass positive TEZ/mutez amount to the _**send()**_** ** method in case of FA1.2/TEZ or FA2/TEZ liquidity investment (see example below).

Also don't forget to add the [DexCore](../../) contract as the operator for your FA2 tokens or make an approve for spending of FA1.2 tokens in time of liquidity investment.
{% endhint %}

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    pair_id: 0,
    token_a_in: 100,
    token_b_in: 100,
    shares: 100,
    shares_receiver: "tz1.../KT1...",
    candidate: "tz1...",
    deadline: String(Date.parse((await tezos.rpc.getBlockHeader()).timestamp) / 1000 + 100),
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.invest_liquidity(parmas).send({ amount: parmas.token_b_in, mutez: true });

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Pass `candidate: "tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg"`in case of TOK/TOK exchange
{% endhint %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `109` - pair doesn't have a liquidity.
* `110` - zero amount of LP tokens (shares) expected.
* `111` - low token A amount in.
* `112` - low token B amount in.
* `136` - reentrancy.
* `141` - wrong amount of TEZ tokens were attached to transaction.
* `144` - action outdated (the time until which the transaction remained valid was passed).
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint). Only in case of investment to TOK/TOK liquidity pools (pairs).
