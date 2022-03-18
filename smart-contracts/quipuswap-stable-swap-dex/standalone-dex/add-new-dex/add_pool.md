# add\_pool

This entrypoint allows `admin` creating a new DEX pool.

{% hint style="info" %}
Underlying tokens should be approved (updated operators) before calling this method.
{% endhint %}

### Call parameters

| Field         |                  Type                 | Description                                                |
| ------------- | :-----------------------------------: | ---------------------------------------------------------- |
| a\_constant   |                 `nat`                 | "A" constant                                               |
| input\_tokens |             `set(token_t)`            | set of tokens inside the future pool (from 2 to 4 entries) |
| tokens\_info  | `map(token_pool_idx_t, token_info_t)` | map of rates config and amount of initial pool reserves    |

```pascaligo
type init_param_t       is [@layout:comb] record [
  a_constant              : nat;
  input_tokens            : set(token_t);
  tokens_info             : map(token_pool_idx_t, token_info_t);
]
```

{% hint style="warning" %}
This contract method is called only by `admin` of that contract.
{% endhint %}
