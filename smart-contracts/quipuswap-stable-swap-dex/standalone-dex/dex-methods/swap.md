# swap

This entrypoint is designed to swap tokens by a specific DEX.

### Call parameters

| Field            |        Type        | Description                                                                                                              |
| ---------------- | :----------------: | ------------------------------------------------------------------------------------------------------------------------ |
| pool\_id         |        `nat`       | pool identifier.                                                                                                         |
| idx\_from        | `token_pool_idx_t` | index of input token.                                                                                                    |
| idx\_to          | `token_pool_idx_t` | index of output token.                                                                                                   |
| amount           |        `nat`       | amount of input token.                                                                                                   |
| min\_amount\_out |        `nat`       | minimal amount of output token expected to receive.                                                                      |
| deadline         |     `timestamp`    | deadline of current operation.                                                                                           |
| receiver         |  `option(address)` | optional, address of the receiver of the LP tokens. If not provided the `sender` address will be used.                   |
| referral         |  `option(address)` | optional, address of the referral of the current operation. If not provided the `default_referral` address will be used. |

```pascaligo
type swap_param_t       is [@layout:comb] record [
  pool_id                 : nat; 
  idx_from                : token_pool_idx_t;
  idx_to                  : token_pool_idx_t;
  amount                  : nat;
  min_amount_out          : nat;
  deadline                : timestamp; 
  receiver                : option(address); 
  referral                : option(address);
]
```
