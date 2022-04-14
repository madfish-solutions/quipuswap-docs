# get\_total\_supply

This on-chain view returns total amount of LP tokens in a specific liquidity pool (pair). Also can return a list of responses for a list of requests.

### Call parameters

```pascaligo
type token_id_t         is nat

type total_supply_req_t is token_id_t

list(total_supply_req_t)
```

| Field                 | Type               | Description                                              |
| --------------------- | ------------------ | -------------------------------------------------------- |
| total\_supply\_req\_t | token\_id\_t (nat) | Pair ID for which you need to get LP tokens total supply |

### Return type

```pascaligo
type token_id_t         is nat

type total_supply_req_t is token_id_t

type total_supply_res_t is [@layout:comb] record [
  request                 : total_supply_req_t;
  total_supply            : nat;
]

list(total_supply_res_t)
```

#### total\_supply\_res\_t

| Field         | Type                        | Description                                              |
| ------------- | --------------------------- | -------------------------------------------------------- |
| request       | total\_supply\_req\_t (nat) | Pair ID for which you need to get LP tokens total supply |
| total\_supply | nat                         | Amount of LP tokens in a liquidity pool (pair)           |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = [0, 1, 15];
const viewCaller = "tz1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const totalSupply = await dexCore.contract.contractViews.get_total_supply(params).executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
