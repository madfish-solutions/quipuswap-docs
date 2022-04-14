# get\_toks\_per\_share

This on-chain view returns amount of token A and token B for the specified amount of LP tokens in a specific liquidity pool (pair). Also can return a list of responses for a list of requests.

### Call parameters

```pascaligo
type token_id_t         is nat

type toks_per_shr_req_t is [@layout:comb] record [
  pair_id                 : token_id_t;
  shares_amt              : nat;
]

list(toks_per_shr_req_t)
```

| Field       | Type               | Description                                                |
| ----------- | ------------------ | ---------------------------------------------------------- |
| pair\_id    | token\_id\_t (nat) | Pair ID for which you need to get tokens amount per shares |
| shares\_amt | nat                | Amount of shares to get info about tokens                  |

### Return type

```pascaligo
type token_id_t         is nat

type toks_per_shr_t     is [@layout:comb] record [
  token_a_amt             : nat;
  token_b_amt             : nat;
]

type toks_per_shr_req_t is [@layout:comb] record [
  pair_id                 : token_id_t;
  shares_amt              : nat;
]

type toks_per_shr_res_t is [@layout:comb] record [
  request                 : toks_per_shr_req_t;
  tokens_per_share        : toks_per_shr_t;
]

list(toks_per_shr_res_t)
```

#### toks\_per\_shr\_req\_t

| Field       | Type               | Description                                                |
| ----------- | ------------------ | ---------------------------------------------------------- |
| pair\_id    | token\_id\_t (nat) | Pair ID for which you need to get tokens amount per shares |
| shares\_amt | nat                | Amount of shares to get info about tokens                  |

#### toks\_per\_shr\_t

| Field         | Type | Description                   |
| ------------- | ---- | ----------------------------- |
| token\_a\_amt | nat  | Amount of tokens A per shares |
| token\_b\_amt | nat  | Amount of tokens B per shares |

#### toks\_per\_shr\_res\_t

| Field              | Type                                                                      | Description                |
| ------------------ | ------------------------------------------------------------------------- | -------------------------- |
| request            | [toks\_per\_shr\_req\_t](get\_toks\_per\_share.md#toks\_per\_shr\_req\_t) | Tokens per shares request  |
| tokens\_per\_share | [toks\_per\_shr\_t](get\_toks\_per\_share.md#toks\_per\_shr\_t)           | Tokens per shares response |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = [
    {
        pair_id: 1,
        shares_amt: 100,
    },
    ...
];
const viewCaller = "tz1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const tokensPerShares = await dexCore.contract.contractViews.get_toks_per_share(params).executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `109` - pair doesn't have a liquidity.
