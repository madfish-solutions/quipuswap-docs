# divest\_imbalanced

This entrypoint is designed to remove liquidity to receive specific underlying assets from the DEX pool.

### Call parameters

| Field        |             Type             | Description                                                                                                              |
| ------------ | :--------------------------: | ------------------------------------------------------------------------------------------------------------------------ |
| pool\_id     |             `nat`            | pool identifier.                                                                                                         |
| amounts\_out | `map(token_pool_idx_t, nat)` | amount of tokens to be received. NOTE: must be provided **at least one** of indexes of tokens                            |
| max\_shares  |             `nat`            | maximum amount of LP tokens to be burnt.                                                                                 |
| deadline     |          `timestamp`         | dealine of current operation.                                                                                            |
| receiver     |       `option(address)`      | optional, address of the receiver of the LP tokens. If not provided the `sender` address will be used.                   |
| referral     |       `option(address)`      | optional, address of the referral of the current operation. If not provided the `default_referral` address will be used. |

```pascaligo
type divest_imb_param_t is [@layout:comb] record [
  pool_id                 : nat;
  amounts_out             : map(token_pool_idx_t, nat);
  max_shares              : nat; 
  deadline                : timestamp; 
  receiver                : option(address); 
  referral                : option(address);
]
```
