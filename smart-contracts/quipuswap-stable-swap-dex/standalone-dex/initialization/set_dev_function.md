# set\_dev\_function

Method for set devloper functions, from [developer-module](../../developer-module/ "mention").

There are 2 functions that belongs to [developer-setter-entrypoints](../../developer-module/developer-setter-entrypoints/ "mention").

```pascaligo
0n -> set_dev_address
1n -> set_dev_fee
```

### Input param type

```pascaligo
type set_lambda_func_t  is [@layout:comb] record [
  func                    : bytes; (* code of the function *)
  index                   : nat; (* the key in functions map *)
]
```

{% hint style="warning" %}
This contract method are called only by `admin` of that contract.&#x20;

For the Factory contract `developer` is `admin.`
{% endhint %}
