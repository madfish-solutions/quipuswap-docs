# add\_rem\_managers

{% hint style="warning" %}
This entrypoint should be called only by `admin` address.
{% endhint %}

This entrypoint is designed to add or remove manager address.&#x20;

**Manager** - `address`, allowed to change metadata of any LP token.

### Call parameters

| Field     |    Type   | Description                                   |
| --------- | :-------: | --------------------------------------------- |
| add       |   `bool`  | `True` to add or `False` to remove candidate. |
| candidate | `address` | address of the candidate manager.             |

```pascaligo
type set_man_param_t    is [@layout:comb] record [
  add                     : bool;
  candidate               : address;
]
```
