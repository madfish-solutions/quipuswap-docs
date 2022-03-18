# set\_token\_function

Method for set FA2 interface functions.

There are 7 functions that belong to [dex-methods](../dex-methods/ "mention").

```pascaligo
0n -> transfer_ep
1n -> get_balance_of
2n -> update_operators
3n -> update_token_metadata
4n -> total_supply_view
```

### Input parameters type

| Field |   Type  | Description                                                                                                          |
| ----- | :-----: | -------------------------------------------------------------------------------------------------------------------- |
| func  | `bytes` | <p>Packed bytes from </p><p><code>type token_func_t is (token_action_t * full_storage_t) -> full_return_t</code></p> |
| index |  `nat`  | Index of the passed method to be set to the lambdas big\_map                                                         |

```pascaligo
type token_action_t     is
| Transfer                of transfer_param_t
| Balance_of              of bal_fa2_param_t
| Update_operators        of operator_param_t
| Update_metadata         of upd_meta_param_t
| Total_supply            of ts_v_param_t

type full_return_t      is list(operation) * full_storage_t
type token_func_t       is (token_action_t * full_storage_t) -> full_return_t

type set_lambda_func_t  is [@layout:comb] record [
  func                    : bytes;
  index                   : nat;
]
```

{% hint style="warning" %}
This contract method is called only by `admin` of that contract.
{% endhint %}
