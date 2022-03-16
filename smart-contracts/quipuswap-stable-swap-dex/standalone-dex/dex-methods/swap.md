# swap

This entrypoint designed to swap tokens by a specific DEX.

### Call params

```pascaligo
type swap_param_t       is [@layout:comb] record [
  pool_id                 : nat; 
  (* pool identifier *)
  idx_from                : token_pool_idx_t;
  (* token index inside pool to be sent to swap *)
  idx_to                  : token_pool_idx_t;
  (* token index inside pool to be received from swap *)
  amount                  : nat;
  (* token amount to be sent to swap *)
  min_amount_out          : nat;
  (* minimal token amount to be received from swap *)
  deadline                : timestamp; 
  (* deadline of operation *)
  receiver                : option(address); 
  (* receiver of LP tokens. If not provided, sender address will be used *)
  referral                : option(address);
  (* referral address. If not provided, default_referral address will be used *)
]
```
