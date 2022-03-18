# invest

This entrypoint is designed to add liquidity to a specific DEX pool.

This method includes a balanced and imbalanced ways of investing.

### Call parameters

| Field       |             Type             | Description                                                                                                              |
| ----------- | :--------------------------: | ------------------------------------------------------------------------------------------------------------------------ |
| pool\_id    |             `nat`            | pool identifier                                                                                                          |
| shares      |             `nat`            | the minimal amount of shares to receive                                                                                  |
| in\_amounts | `map(token_pool_idx_t, nat)` | map of token amounts to be invested                                                                                      |
| deadline    |          `timestamp`         | dealine of current operation                                                                                             |
| receiver    |       `option(address)`      | optional, address of the receiver of the LP tokens. If not provided the `sender` address will be used.                   |
| referral    |       `option(address)`      | optional, address of the referral of the current operation. If not provided the `default_referral` address will be used. |

```pascaligo
type invest_param_t     is [@layout:comb] record [
  pool_id                 : nat; 
  shares                  : nat; 
  in_amounts              : map(token_pool_idx_t, nat); 
  deadline                : timestamp; 
  receiver                : option(address); 
  referral                : option(address);
]
```
