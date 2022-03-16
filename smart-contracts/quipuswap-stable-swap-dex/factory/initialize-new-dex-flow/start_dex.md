# start\_dex

This entrypoint allows `deployer` finish setup of a new DEX pool.

Deployed pool searched by sender address (`deployer`) and passed to call tokens of `token_t` type.

{% hint style="info" %}
Underlying tokens should be approved (updated operators) before calling this method.
{% endhint %}

### Call params

```pascaligo
type input_t_v_t        is [@layout:comb] record [
  token                   : token_t; // FA12/FA2 token
  value                   : nat; // amount of token to invest
]

type start_dex_param_t  is map(nat, input_t_v_t) 
(* mapping of token index in pool to token-amount values *)
```

{% hint style="warning" %}
This contract method is called only by `deployer` that called [add\_pool.md](add\_pool.md "mention").
{% endhint %}
