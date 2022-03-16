# set\_admin\_function

Method for set admin functions.

There are 8 functions that belongs to admin methods in Standalone variant and 7 functions in Factory variant (`add_pool` [add-new-dex](../add-new-dex/ "mention") excluded from Factory variant).

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
