# divest

This entrypoint is designed to remove liquidity from a specific DEX pool in balanced way.

### Call params

```pascaligo
type divest_param_t     is [@layout:comb] record [
  pool_id                 : nat;
  (* pool identifier *)
  min_amounts_out         : map(token_pool_idx_t, nat);
  (* min amount of tokens to be received. NOTE: must be provided all of indexes of tokens *)
  shares                  : nat; 
  (* amount of shares to be burnt *)
  deadline                : timestamp; 
  (* deadline of operation *)
  receiver                : option(address); 
  (* receiver of tokens. If not provided, sender address will be used *)
]
```
