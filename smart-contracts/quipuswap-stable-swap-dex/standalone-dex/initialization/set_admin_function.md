# set\_admin\_function

Method for set admin functions.

There are 8 functions that belong to admin methods in the Standalone variant and 7 functions in the Factory variant (`add_pool` [add-new-dex](../add-new-dex/ "mention") excluded from Factory variant).

```pascaligo
0n -> add_rem_managers
1n -> set_admin
2n -> claim_dev // called by developer address, check for admin address skipped
3n -> ramp_A
4n -> stop_ramp_A
5n -> set_fees
6n -> set_default_referral
7n -> add_pool // excluded in Factory implementation
```

### Input parameters type

| Field |   Type  | Description                                                                                                |
| ----- | :-----: | ---------------------------------------------------------------------------------------------------------- |
| func  | `bytes` | <p>Packed bytes from </p><p><code>type admin_func_t is (admin_action_t * storage_t) -> return_t</code></p> |
| index |  `nat`  | Index of the passed method to be set to the lambdas big\_map                                               |

```pascaligo
type admin_action_t     is
| Add_rem_managers        of set_man_param_t
| Set_admin               of address
| Claim_developer         of claim_by_token_param_t
| Ramp_A                  of ramp_a_param_t
| Stop_ramp_A             of nat
| Set_fees                of set_fee_param_t
| Set_default_referral    of address
#if !FACTORY // flag separates stanalone and factory implementations
| Add_pool                of init_param_t
#endif


type return_t           is list(operation) * storage_t
type admin_func_t       is (admin_action_t * storage_t) -> return_t

type set_lambda_func_t  is [@layout:comb] record [
  func                    : bytes;
  index                   : nat;
]
```

{% hint style="warning" %}
This contract method is called only by `admin` of that contract.
{% endhint %}
