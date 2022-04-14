# get\_swap\_min\_res

This on-chain view returns a minimum result (output) of a swap.

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

type get_swap_min_res_t is [@layout:comb] record [
  swaps                   : list(swap_slice_t);
  amount_in               : nat;
]
```

#### swap\_slice\_t

| Field     | Type               | Description                                 |
| --------- | ------------------ | ------------------------------------------- |
| direction | swap\_direction\_t | Swap direction: A->B or B->A                |
| pair\_id  | token\_id\_t (nat) | ID of a pair in which swap will be executed |

#### get\_swap\_min\_res\_t

| Field      | Type                                                          | Description                   |
| ---------- | ------------------------------------------------------------- | ----------------------------- |
| swaps      | list([swap\_slice\_t](get\_swap\_min\_res.md#swap\_slice\_t)) | A route of a swap             |
| amount\_in | nat                                                           | Amount of tokens to swap from |

### Return type

```pascaligo
nat
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = {
    swaps: [
        {
            direction: {
                a_to_b: undefinded,
            },
            pair_id: 1,
        },
        ...
    ],
    amount_in: 1000,
};
const viewCaller = "tz1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const swapMinRes = await dexCore.contract.contractViews.get_swap_min_res(params).executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `109` - pair doesn't have a liquidity.
* `113` - a [Bucket](../../bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `117` - empty route of swaps.
* `118` - zero amount in was passed as the parameter.
* `119` - wrong route of a swap.
