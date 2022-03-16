# add\_pool

This entrypoint allows `admin` creating a new DEX pool.

{% hint style="info" %}
Underlying tokens should be approved (updated operators) before calling this method.
{% endhint %}

### Call params

```pascaligo
type init_param_t       is [@layout:comb] record [
  a_constant              : nat;
  input_tokens            : set(token_t);
  tokens_info             : map(token_pool_idx_t, token_info_t);
]
```

{% hint style="warning" %}
This contract method are called only by `admin` of that contract.
{% endhint %}
