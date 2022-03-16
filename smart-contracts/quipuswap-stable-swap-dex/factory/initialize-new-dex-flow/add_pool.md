# add\_pool

This entrypoint allows anyone to deploy a new own DEX pool.

{% hint style="info" %}
QUIPU token should be approved (updated operators) before calling this method.
{% endhint %}

### Call params

Parameters logically close to Standalone variant of [add-new-dex](../../standalone-dex/add-new-dex/ "mention"), but there is no "`reserves`" field in tokens\_info mapping (because invest performs at second step - [start\_dex.md](start\_dex.md "mention")) and some additional config parameters.

* `default_referral` - the address that would be the default referral at the new pool.
* `managers` - set of addresses that allowed to manipulate LP token metadata at the new pool.
* `metadata` - metadata of deployed contract.
* `token_metadata`  - metadata of the LP token at the new pool.

```pascaligo
type token_prec_info_t  is [@layout:comb] record [
  rate                    : nat;
  precision_multiplier    : nat;
]

type pool_init_param_t  is [@layout:comb] record [
  a_constant              : nat; // A*n^(n-1)
  input_tokens            : set(token_t);
  tokens_info             : map(token_pool_idx_t, token_prec_info_t);
  default_referral        : address;
  managers                : set(address);
  metadata                : big_map(string, bytes);
  token_metadata          : big_map(token_id_t, token_meta_info_t);
]
```
