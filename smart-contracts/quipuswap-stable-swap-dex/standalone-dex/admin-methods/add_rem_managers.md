# add\_rem\_managers

{% hint style="warning" %}
This entrypoint should be called only by `admin` address.
{% endhint %}

This entrypoint is designed to add or remove manager address.&#x20;

**Manager** - `address`, allowed to change metadata of any LP token.

### Call params

```pascaligo
type set_man_param_t    is [@layout:comb] record [
  add                     : bool; // add or remove flag
  candidate               : address; // address that need add/remove
]
```
