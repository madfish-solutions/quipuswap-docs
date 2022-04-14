# swap

An entrypoint that executes swaps in different liquidity pools (pairs).

All possible routes for swaps are allowed. For example: `FA1.2->TEZ`, `TEZ->FA1.2`, `FA2->TEZ`, `TEZ->FA2`, `FA1.2->FA1.2`, `FA2->FA2`, `FA1.2->FA2`, `FA2->FA1.2`.

Multi token routes are allowed too. For example: `FA1.2->FA2->TEZ->FA2`, `TEZ->FA2->FA1.2->TEZ`, `FA2->TEZ->FA2->TEZ->FA1.2`.

### Call parameters

```pascaligo
type token_id_t         is nat

type swap_direction_t   is
| A_to_b
| B_to_a

type swap_slice_t       is [@layout:comb] record [
  direction               : swap_direction_t;
  pair_id                 : token_id_t;
]

type swap_t             is [@layout:comb] record [
  swaps                   : list(swap_slice_t);
  deadline                : timestamp;
  receiver                : address;
  referrer                : address;
  amount_in               : nat;
  min_amount_out          : nat;
]
```

#### swap\_slice\_t

| Field     | Type               | Description                                 |
| --------- | ------------------ | ------------------------------------------- |
| direction | swap\_direction\_t | Swap direction: A->B or B->A                |
| pair\_id  | token\_id\_t (nat) | ID of a pair in which swap will be executed |

#### get\_swap\_min\_res\_t

| Field            | Type                                           | Description                                                                 |
| ---------------- | ---------------------------------------------- | --------------------------------------------------------------------------- |
| swaps            | list([swap\_slice\_t](swap.md#swap\_slice\_t)) | A route of a swap                                                           |
| deadline         | timestamp                                      | The time until which the transaction remains valid and will not be rejected |
| receiver         | address                                        | The receiver of exchanged tokens                                            |
| referrer         | address                                        | Referrer to whom interface fee will be paid                                 |
| amount\_in       | nat                                            | Amount of tokens to swap from                                               |
| min\_amount\_out | nat                                            | The minimum number of outgoing tokens that the user agrees to               |

### Usage

{% hint style="danger" %}
You need to pass positive TEZ/mutez amount to the _**send()**_** ** method in case of TEZ->FA1.2 or TEZ -> FA2 swaps (see example below).

Also don't forget to add the [DexCore](../../) contract as the operator for your FA2 tokens or make an approve for spending of FA1.2 tokens in time of FA1.2/FA2->FA1.2/FA2/TEZ swaps.
{% endhint %}

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const parmas = {
    swaps: [
        {
            direction: {
                a_to_b: undefinded,
            },
            pair_id: 1,
        },
        ...
    ],
    deadline: String(Date.parse((await tezos.rpc.getBlockHeader()).timestamp) / 1000 + 100),
    receiver: "tz1.../KT1...",
    referrer: "tz1.../KT1...",
    amount_in: 1000,
    min_amount_out: 998,
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.swap(parmas).send({ amount: parmas.amount_in, mutez: true });

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `109` - pair doesn't have a liquidity.
* `116` - high expectations of output tokens.
* `117` - empty route of swaps.
* `118` - zero amount in was passed as the parameter.
* `119` - wrong route of a swap.
* `120` - wrong TEZ amount were passed to the transaction.
* `130` - referring on yourself is forbidden.
* `136` - reentrancy.
* `139` - too few swaps.
* `144` - action outdated (the time until which the transaction remained valid was passed).
