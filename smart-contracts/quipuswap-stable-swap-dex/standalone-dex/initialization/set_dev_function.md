# set\_dev\_function

Method for set developer functions, from [developer-module](../../developer-module/ "mention").

There are 2 functions that belong to [developer-setter-entrypoints](../../developer-module/developer-setter-entrypoints/ "mention").

```pascaligo
0n -> set_dev_address
1n -> set_dev_fee
```

### Input parameters type

| Field |   Type  | Description                                                                                                     |
| ----- | :-----: | --------------------------------------------------------------------------------------------------------------- |
| func  | `bytes` | <p>Packed bytes from </p><p><code>type dev_func_t is (dev_action_t * dev_storage_t) -> dev_storage_t</code></p> |
| index |  `nat`  | Index of the passed method to be set to the `dev_lambdas` big\_map                                              |

```pascaligo
type dev_action_t       is
| Set_dev_address         of address
| Set_dev_fee             of nat

type dev_storage_t      is [@layout:comb] record [
  dev_address             : address;
  dev_fee_f               : nat;
  dev_lambdas             : big_map(nat, bytes);
]

type dev_func_t         is (dev_action_t * dev_storage_t) -> dev_storage_t

type set_lambda_func_t  is [@layout:comb] record [
  func                    : bytes;
  index                   : nat;
]
```

{% hint style="warning" %}
This contract method are called only by `admin` of that contract.&#x20;

For the Factory contract `developer` is `admin.`
{% endhint %}
