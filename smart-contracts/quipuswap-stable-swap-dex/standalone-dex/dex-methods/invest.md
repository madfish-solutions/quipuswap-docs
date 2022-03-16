# invest

This entrypoint designed to add liquidity to a specific DEX pool.

This method includes balanced and imbalanced way of investing.

### Call params

```pascaligo
type invest_param_t     is [@layout:comb] record [
  pool_id                 : nat; 
  (* pool identifier *)
  shares                  : nat; 
  (* the minimal amount of shares to receive *)
  in_amounts              : map(token_pool_idx_t, nat); 
  (* amount of tokens mapping to be invested *)
  deadline                : timestamp; 
  (* deadline of operation *)
  receiver                : option(address); 
  (* receiver of LP tokens. If not provided, sender address will be used *)
  referral                : option(address);
  (* referral address. If not provided, default_referral address will be used *)
]
```
