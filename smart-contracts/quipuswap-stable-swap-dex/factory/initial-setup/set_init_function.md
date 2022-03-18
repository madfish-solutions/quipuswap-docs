# set\_init\_function

Method for set DEX contract deployer function lambda.

Deployer function deploys new DEX contract to the blockchain with copied admin and token lambdas and charges deploy fee in QUIPU tokens. Part of fees stays inside contact reserves (`quipu_rewards`) and the other part goes to "burn address" - hardcoded zero-address to burn QUIPU tokens.

Input param type is `bytes`.

### Parameters

| Field |   Type  | Description                                                                                   |
| ----- | :-----: | --------------------------------------------------------------------------------------------- |
| -     | `bytes` | packed bytes from `type init_func_t is (pool_init_param_t * full_storage_t) -> fact_return_t` |

```pascaligo
type pool_init_param_t  is [@layout:comb] record [
  a_constant              : nat;
  input_tokens            : set(token_t);
  tokens_info             : map(token_pool_idx_t, token_prec_info_t);
  default_referral        : address;
  managers                : set(address);
  metadata                : big_map(string, bytes);
  token_metadata          : big_map(token_id_t, token_meta_info_t);
]

type fact_return_t      is list(operation) * full_storage_t

type init_func_t        is (pool_init_param_t * full_storage_t) -> fact_return_t
```

{% hint style="warning" %}
This contract method is called only by `developer` of that contract.
{% endhint %}
