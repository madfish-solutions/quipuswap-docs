# get\_reserves

This on-chain view returns reserves (token A and token B) in a specific liquidity pool (pair). Also can return a list of responses for a list of requests.

### Call parameters

```pascaligo
type token_id_t         is nat

type reserves_req_t     is token_id_t

list(reserves_req_t)
```

| Field            | Type               | Description                                |
| ---------------- | ------------------ | ------------------------------------------ |
| reserves\_req\_t | token\_id\_t (nat) | Pair ID for which you need to get reserves |

### Return type

```pascaligo
type token_id_t         is nat

type reserves_t         is [@layout:comb] record [
  token_a_pool            : nat;
  token_b_pool            : nat;
]

type reserves_req_t     is token_id_t

type reserves_res_t     is [@layout:comb] record [
  request                 : reserves_req_t;
  reserves                : reserves_t;
]

list(reserves_res_t)
```

#### reserves\_t

| Field          | Type | Description                                    |
| -------------- | ---- | ---------------------------------------------- |
| token\_a\_pool | nat  | Amount of token A in the liquidity pool (pair) |
| token\_b\_pool | nat  | Amount of token B in the liquidity pool (pair) |

#### reserves\_res\_t

| Field    | Type                                        | Description                                   |
| -------- | ------------------------------------------- | --------------------------------------------- |
| request  | reserves\_req\_t (nat)                      | Pair ID for which you need to get a reserves  |
| reserves | [reserves\_t](get\_reserves.md#reserves\_t) | Reserves of tokens in a liquidity pool (pair) |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = [0, 1, 15];
const viewCaller = "tz1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const reserves = await dexCore.contract.contractViews.get_reserves(params).executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
