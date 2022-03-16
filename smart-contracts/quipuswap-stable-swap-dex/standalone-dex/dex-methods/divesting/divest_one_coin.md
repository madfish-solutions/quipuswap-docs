# divest\_one\_coin

This entrypoint is designed to remove liquidity from a specific DEX pool in one underlying token.

### Call params

```pascaligo
type divest_one_c_param_t is [@layout:comb] record [
  pool_id                 : nat;
  (* pool identifier *)
  shares                  : nat;
  (* amount of LP tokens to be burnt *)
  token_index             : token_pool_idx_t;
  (* index of token in pool to withdraw *)
  min_amount_out          : nat;
  (* min amount of tokens to be received *)
  deadline                : timestamp; 
  (* deadline of operation *)
  receiver                : option(address); 
  (* receiver of tokens. If not provided, sender address will be used *)
  referral                : option(address);
  (* referral address. If not provided, default_referral address will be used *)
]
```

{% hint style="danger" %}
The parameter `shares` provided to call, that represents amount LP tokens would be burnt **in full**. So, if you want to burn more LP tokens **by value** than available reserves of selected underlying token, than you could **lost some of your liquidity**.
{% endhint %}
