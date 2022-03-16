# set\_dex\_function

Method for set dex core functions.

There are 7 functions that belongs to [dex-methods](../dex-methods/ "mention").

```pascaligo
0n -> swap
1n -> invest_liquidity
2n -> divest_liquidity
3n -> divest_imbalanced
4n -> divest_one_coin
5n -> claim_ref
6n -> stake
```

### Input param type

```pascaligo
type set_lambda_func_t  is [@layout:comb] record [
  func                    : bytes; (* code of the function *)
  index                   : nat; (* the key in functions map *)
]
```

{% hint style="warning" %}
This contract method are called only by `admin` of that contract.
{% endhint %}
