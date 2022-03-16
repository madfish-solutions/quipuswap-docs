# 📄 Storage & action types

### Developer actions

Action type for module setters.

{% content-ref url="developer-setter-entrypoints/" %}
[developer-setter-entrypoints](developer-setter-entrypoints/)
{% endcontent-ref %}

```pascaligo
type dev_action_t       is
| Set_dev_address         of address
| Set_dev_fee             of nat
```

### Developer storage

| Field        |          Type         | Hint                                           | Description                |
| ------------ | :-------------------: | ---------------------------------------------- | -------------------------- |
| dev\_address |       `address`       |                                                | Address of developer       |
| dev\_fee     |         `nat`         | (float) multiplied by `fee_denominator` (1e10) | fee rate that goes to dev. |
| dev\_lambdas | `big_map(nat, bytes)` |                                                | Developer action lambdas   |

```pascaligo
type dev_storage_t      is [@layout:comb] record [
  dev_address             : address;
  dev_fee                 : nat;
  dev_lambdas             : big_map(nat, bytes);
]
```

#### Lambda type

Lambda is stored as `bytes`, packed from `dev_func_t`.

```pascaligo
type dev_func_t is (dev_action_t * dev_storage_t) -> dev_storage_t
```
