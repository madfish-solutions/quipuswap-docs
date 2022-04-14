# divest\_liquidity

An entrypoint for liquidity divestment from the specific liquidity pool (pair). Also it [votes](../../../bucket-contract/entrypoints-overview/vote.md) for the users' bakers in case of liquidity divestment from TOK/TEZ pools.

### Call parameters

```pascaligo
type token_id_t         is nat

type divest_liquidity_t is [@layout:comb] record [
  pair_id                 : token_id_t;
  min_token_a_out         : nat;
  min_token_b_out         : nat;
  shares                  : nat;
  liquidity_receiver      : address;
  candidate               : key_hash;
  deadline                : timestamp;
]
```

| Field               | Type               | Description                                                                  |
| ------------------- | ------------------ | ---------------------------------------------------------------------------- |
| pair\_id            | token\_id\_t (nat) | Identifier of the liquidity pool (pair)                                      |
| min\_token\_a\_out  | nat                | The minimum number of token A that the user agrees to                        |
| min\_token\_b\_out  | nat                | The minimum number of token B that the user agrees to                        |
| shares              | nat                | Amount of LP tokens to use in time of divestment                             |
| liquidity\_receiver | address            | Receiver of tokens A and tokens B                                            |
| candidate           | key\_hash          | Baker for voting (is used only in time of divestment from TOK/TEZ exchanges) |
| deadline            | timestamp          | The time until which the transaction remains valid and will not be rejected  |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    pair_id: 0,
    min_token_a_out: 100,
    min_token_b_out: 100,
    shares: 100,
    liquidity_receiver: "tz1.../KT1...",
    candidate: "tz1...",
    deadline: String(Date.parse((await tezos.rpc.getBlockHeader()).timestamp) / 1000 + 100),
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.divest_liquidity(parmas).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `109` - pair doesn't have a liquidity.
* `114` - insufficient liquidity.
* `115` - dust output (zero tokens amount expected).
* `116` - high expectations of output tokens.
* `136` - reentrancy.
* `142` - wrong reserves state after execution of the operation.
* `144` - action outdated (the time until which the transaction remained valid was passed).
