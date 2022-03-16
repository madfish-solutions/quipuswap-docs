# set\_token\_function

Method for set FA2 interface functions.

There are 7 functions that belongs to [dex-methods](../dex-methods/ "mention").

```pascaligo
0n -> transfer_ep
1n -> get_balance_of // old-style view
2n -> update_operators
3n -> update_token_metadata // udpdate metadata performs by LP token manager
4n -> total_supply_view //old-style view
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
