# divest

This entrypoint is designed to remove liquidity from a specific DEX pool according to current exchange rate.

### Call parameters

| Field             |             Type             | Description                                                                                            |
| ----------------- | :--------------------------: | ------------------------------------------------------------------------------------------------------ |
| pool\_id          |             `nat`            | pool identifier.                                                                                       |
| min\_amounts\_out | `map(token_pool_idx_t, nat)` | min amount of tokens to be received. NOTE: must be provided **all** indexes of tokens                  |
| shares            |             `nat`            | amount of LP token to be burn.                                                                         |
| deadline          |          `timestamp`         | dealine of current operation.                                                                          |
| receiver          |       `option(address)`      | optional, address of the receiver of the LP tokens. If not provided the `sender` address will be used. |

```pascaligo
type divest_param_t     is [@layout:comb] record [
  pool_id                 : nat;
  min_amounts_out         : map(token_pool_idx_t, nat);
  shares                  : nat; 
  deadline                : timestamp; 
  receiver                : option(address); 
]
```
