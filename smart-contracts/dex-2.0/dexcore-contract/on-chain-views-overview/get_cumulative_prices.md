# get\_cumulative\_prices

This on-chain view returns cumulative prices and last timestamp of its calculation for a liquidity pool (pair). Also can return a list of cumulative prices for a list of liquidity pools.

### Call parameters

```pascaligo
type token_id_t         is nat

type cum_prices_req_t   is token_id_t

list(cum_prices_req_t)
```

| Field               | Type               | Description                                         |
| ------------------- | ------------------ | --------------------------------------------------- |
| cum\_prices\_req\_t | token\_id\_t (nat) | Pair ID for which you need to get cumulative prices |

### Return type

```pascaligo
type token_id_t         is nat

type cum_prices_t       is [@layout:comb] record [
  last_block_timestamp    : timestamp;
  token_a_price_cml       : nat;
  token_b_price_cml       : nat;
]

type cum_prices_req_t   is token_id_t

type cum_prices_res_t   is [@layout:comb] record [
  request                 : cum_prices_req_t;
  cumulative_prices       : cum_prices_t;
]

list(cum_prices_res_t)
```

#### cum\_prices\_t

| Field                  | Type      | Description                                     |
| ---------------------- | --------- | ----------------------------------------------- |
| last\_block\_timestamp | timestamp | Last timestamp of cumulative prices calculation |
| token\_a\_price\_cml   | nat       | Cumulative price of token A                     |
| token\_b\_price\_cml   | nat       | Cumulative price of token B                     |

#### cum\_prices\_res\_t

| Field              | Type                                                        | Description                |
| ------------------ | ----------------------------------------------------------- | -------------------------- |
| request            | cum\_prices\_req\_t (nat)                                   | Cumulative prices request  |
| cumulative\_prices | [cum\_prices\_t](get\_cumulative\_prices.md#cum\_prices\_t) | Cumulative prices response |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = [0, 1, 15];
const viewCaller = "tz1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const cumulativePrices = await dexCore.contract.contractViews.get_cumulative_prices(params).executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
