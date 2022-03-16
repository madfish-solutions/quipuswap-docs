# divest\_imbalanced

This entrypoint is designed to remove liquidity from a specific DEX pool in imbalanced way.

### Call params

```pascaligo
type divest_imb_param_t is [@layout:comb] record [
  pool_id                 : nat;
  (* pool identifier *)
  amounts_out             : map(token_pool_idx_t, nat);
  (* min amount of tokens to be received NOTE: must be provided at least one of indexes of tokens *)
  max_shares              : nat; 
  (* maximum amount of LP tokens to be burnt *)
  deadline                : timestamp; 
  (* deadline of operation *)
  receiver                : option(address); 
  (* receiver of tokens. If not provided, sender address will be used *)
  referral                : option(address);
  (* referral address. If not provided, default_referral address will be used *)
]
```
