# launch\_exchange

An entrypoint that launches a new exchanges. Next types of exchanges are supported:

* FA1.2/FA1.2;
* FA1.2/FA2;
* FA1.2/TEZ;
* FA2/FA1.2;
* FA2/FA2;
* FA2/TEZ;
* TEZ/FA1.2;
* TEZ/FA2.

In case of TOK/TEZ exchange launch [voting](../../../bucket-contract/entrypoints-overview/vote.md) in appropriative [Bucket](../../../bucket-contract/) contract is executed. Also all TEZ tokens is [transferred](../../../bucket-contract/entrypoints-overview/fill.md) to the same [Bucket](../../../bucket-contract/) contract before voting.

In time of first exchange launch, this contract calls [_**launch\_callback**_](../callbacks/launch\_callback.md) entrypoint. This is done in order to vote on a [Bucket](../../../bucket-contract/) contract that has just been deployed and cannot be accessed until the launch exchange transaction completes. Therefore, voting takes place in the next transaction, sent from [_**launch\_callback**_](../callbacks/launch\_callback.md).

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

type tokens_t           is [@layout:comb] record [
  token_a                 : token_t;
  token_b                 : token_t;
]

type launch_exchange_t  is [@layout:comb] record [
  pair                    : tokens_t;
  token_a_in              : nat;
  token_b_in              : nat;
  shares_receiver         : address;
  candidate               : key_hash;
  deadline                : timestamp;
]
```

#### tokens\_t

| Field    | Type     | Description         |
| -------- | -------- | ------------------- |
| token\_a | token\_t | FA1.2/FA2/TEZ token |
| token\_b | token\_t | FA1.2/FA2/TEZ token |

#### launch\_exchange\_t

| Field            | Type                                       | Description                                                                 |
| ---------------- | ------------------------------------------ | --------------------------------------------------------------------------- |
| pair             | [tokens\_t](launch\_exchange.md#tokens\_t) | Tokens to launch exchange with                                              |
| token\_a\_in     | nat                                        | Amount of token A for investment                                            |
| token\_b\_in     | nat                                        | Amount of token B for investment                                            |
| shares\_receiver | address                                    | Receiver of LP tokens                                                       |
| candidate        | key\_hash                                  | Baker for voting (is used only in time of TOK/TEZ exchanges launch)         |
| deadline         | timestamp                                  | The time until which the transaction remains valid and will not be rejected |

### Usage

{% hint style="danger" %}
Note: you need to pass positive TEZ/mutez amount to the _**send()**_** ** method in case of FA1.2/TEZ or FA2/TEZ exchanges launch (see example below).

Also don't forget to add the [DexCore](../../) contract as the operator for your FA2 tokens or make an approve for spending of FA1.2 tokens in time of exchange launch.
{% endhint %}

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    pair: {
        token_a: {
            fa12: "KT1...",
        }, 
        token_b: {
            tez: undefined,
        },
    },
    token_a_in: 100,
    token_b_in: 100,
    shares_receiver: "tz1.../KT1...",
    candidate: "tz1...",
    deadline: String(Date.parse((await tezos.rpc.getBlockHeader()).timestamp) / 1000 + 100),
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.launch_exchange(parmas).send({ amount: parmas.token_b_in, mutez: true });

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `104` - wrong order of a tokens from parameters.
* `105` - zero token A amount in.
* `106` - zero token B amount in.
* `107` - pair (pool) with the specified `token_id` already listed.
* `120` - wrong TEZ amount were passed to the transaction.
* `136` - reentrancy.
* `144` - action outdated (the time until which the transaction remained valid was passed).
