# set\_dex\_function

Method for set dex core functions.

There are 7 functions that belong to [dex-methods](../dex-methods/ "mention").

```pascaligo
0n -> swap
1n -> invest_liquidity
2n -> divest_liquidity
3n -> divest_imbalanced
4n -> divest_one_coin
5n -> claim_ref
6n -> stake
```

### Input parameters type

| Field |   Type  | Description                                                                                            |
| ----- | :-----: | ------------------------------------------------------------------------------------------------------ |
| func  | `bytes` | <p>Packed bytes from </p><p><code>type dex_func_t is (dex_action_t * storage_t) -> return_t</code></p> |
| index |  `nat`  | Index of the passed method to be set to the lambdas big\_map                                           |

```pascaligo
type dex_action_t       is
(* Base actions *)
| Swap                    of swap_param_t
| Invest                  of invest_param_t
| Divest                  of divest_param_t
(* Custom actions *)
| Divest_imbalanced       of divest_imb_param_t
| Divest_one_coin         of divest_one_c_param_t
| Claim_referral          of claim_by_token_param_t
| Stake                   of stake_action_t

type return_t           is list(operation) * storage_t
type dex_func_t         is (dex_action_t * storage_t) -> return_t

type set_lambda_func_t  is [@layout:comb] record [
  func                    : bytes;
  index                   : nat;
]
```

{% hint style="warning" %}
This contract method is called only by `admin` of that contract.
{% endhint %}
