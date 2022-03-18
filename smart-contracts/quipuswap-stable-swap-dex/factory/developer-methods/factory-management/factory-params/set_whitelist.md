# set\_whitelist

{% hint style="warning" %}
This contract method is called only by `developer` of that contract.
{% endhint %}

This method adds (or removes) addresses to the whitelist (for deploying new pools without charging QUIPU tokens).

### Call parameters

| Field     |    Type   | Description                                   |
| --------- | :-------: | --------------------------------------------- |
| add       |   `bool`  | `True` to add or `False` to remove candidate. |
| candidate | `address` | address of the whitelist candidate.           |

```pascaligo
type set_man_param_t    is [@layout:comb] record [
  add                     : bool;
  candidate               : address;
]
```

