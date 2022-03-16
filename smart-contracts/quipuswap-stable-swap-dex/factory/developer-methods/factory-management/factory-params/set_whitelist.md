# set\_whitelist

{% hint style="warning" %}
This contract method is called only by `developer` of that contract.
{% endhint %}

This method adds (or removes) addresses to the whitelist (for deploying new pools without charging QUIPU tokens).

### Call params

```pascaligo
type set_man_param_t    is [@layout:comb] record [
  add                     : bool;    // add = True, remove = False
  candidate               : address; // address to manipulate with whitelist
]
```

