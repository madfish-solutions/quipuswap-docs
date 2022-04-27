# swap

In the current implementation, under the hood, all swaps are actually flash swaps. This simply means that contract sends output tokens to the recipient before enforcing that enough input tokens have been received. This is slightly atypical, as one might expect a pair to ensure it's received payment before delivery. However, because Tezos transactions are atomic, we can roll back the entire swap if it turns out that the contract hasn't received enough tokens to make itself whole by the end of the transaction.

Below you can find detailed description of both use cases: simple swap and flash swap.

## Swap

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
  lambda                  : option(unit -> list(operation));
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

| Field            | Type                                           | Description                                                                                                                                                           |
| ---------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| lambda           | option(unit -> list(operation))                | Users's lambda function that doesn't accept any parameters (_**unit**_) and returns a list of operations (transactions, calls). Must be `None` in case of simple swap |
| swaps            | list([swap\_slice\_t](swap.md#swap\_slice\_t)) | A route of a swap                                                                                                                                                     |
| deadline         | timestamp                                      | The time until which the transaction remains valid and will not be rejected                                                                                           |
| receiver         | address                                        | The receiver of exchanged tokens                                                                                                                                      |
| referrer         | address                                        | Referrer to whom interface fee will be paid                                                                                                                           |
| amount\_in       | nat                                            | Amount of tokens to swap from                                                                                                                                         |
| min\_amount\_out | nat                                            | The minimum number of outgoing tokens that the user agrees to                                                                                                         |

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
    lambda: undefined, // or null
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
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint). Only in case of swapping NOT from TEZ token.

## Flash swap

An entrypoint that allows to make a flash swaps. QuipuSwap flash swaps allows you to exchange up to the full reserves of any FA1.2/FA2/TEZ token on QuipuSwap and execute arbitrary logic at no upfront cost, provided that by the end of the transaction you will pay for the withdrawn FA1.2/FA2/TEZ tokens with the corresponding pair tokens.

After execution of user's lambda, [_**flash\_swap\_callback**_](../callbacks/flash\_swap\_callback.md) entrypoint will be executed (only in case of TEZ tokens loan).

All possible routes for swaps are allowed. Also, supports multi token routes.

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
  lambda                  : option(unit -> list(operation));
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

| Field            | Type                                           | Description                                                                                                                    |
| ---------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| lambda           | option(unit -> list(operation))                | Users's lambda function that doesn't accept any parameters (_**unit**_) and returns a list of operations (transactions, calls) |
| swaps            | list([swap\_slice\_t](swap.md#swap\_slice\_t)) | A route of a swap                                                                                                              |
| deadline         | timestamp                                      | The time until which the transaction remains valid and will not be rejected                                                    |
| receiver         | address                                        | The receiver of exchanged tokens                                                                                               |
| referrer         | address                                        | Referrer to whom interface fee will be paid                                                                                    |
| amount\_in       | nat                                            | Amount of tokens to swap from                                                                                                  |
| min\_amount\_out | nat                                            | The minimum number of outgoing tokens that the user agrees to                                                                  |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
import { execSync } from "child_process";

function parseSwaps(swaps) {
    let result = "list [ ";

    for (const swap of swaps) {
        const direction =
          Object.keys(swap.direction)[0].charAt(0).toUpperCase() +
          Object.keys(swap.direction)[0].substring(1);
 
        result += `record [ direction = ${direction}; pair_id = ${swap.pair_id.toString()}n; ]; `;
    }

    return result + " ]";
}

const dexCoreAddress = "KT1...";
const mutezAmount = 100;
const params = {
    lambda: undefined,
    swaps: [{ direction: { a_to_b: undefined }, pair_id: 0 }],
    deadline: String(Date.parse((await tezos.rpc.getBlockHeader()).timestamp) / 1000 + 100),
    receiver: "KT1...", // a contract that will execute arbitrary logic or do smth with received tokens
    referrer: "tz1...",
    amount_in: 1000,
    min_amount_out: 1,
};
const stdout = execSync(
    `${ligo} compile parameter ${lambda_file} 'Use(Swap(record [ lambda = Some(${lambda_name}); swaps = ${parseSwaps(
      params.swaps
    )}; deadline = (${params.deadline} : timestamp); receiver = ("${
      params.receiver
    }" : address); referrer = ("${
      params.referrer
    }" : address); amount_in = ${params.amount_in.toString()}n; min_amount_out = ${params.min_amount_out.toString()}n ] ))' -p hangzhou --michelson-format json`,
    { maxBuffer: 1024 * 500 }
).toString();
const operation = await tezos.contract.transfer({
    to: dexCoreAddress,
    amount: mutezAmount,
    mutez: true,
    parameter: {
        entrypoint: "use",
        value: JSON.parse(stdout).args[0],
    },
    fee: 1000000,
    gasLimit: 1040000,
    storageLimit: 20000,
});

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Lambda function example

FlashSwapAgent - contract that implements different arbitrary logic.

```pascaligo
const agent : address = ("KT1LZjpR3hysVYyji1bfgNHJAuZhiQApUd71" : address);
const val : nat = 100n;

function get_flash_swap_agent_default_entrypoint(
  const agent           : address)
                        : contract(nat) is
  Tezos.get_contract_with_error(agent, "FlashSwapAgent/default-entrypoint-404")

function lambda(const _ : unit) : list(operation) is
  list [
    Tezos.transaction(
      val,
      0mutez,
      get_flash_swap_agent_default_entrypoint(agent)
    )
  ]
```

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
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint). Only in case of swapping NOT from TEZ token.
* all errors from the [_**flash\_swap\_callback**_](../callbacks/flash\_swap\_callback.md) entrypoint.
