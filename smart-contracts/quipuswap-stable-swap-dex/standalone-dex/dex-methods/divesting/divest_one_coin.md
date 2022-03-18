# divest\_one\_coin

This entrypoint is designed to remove liquidity from a specific DEX pool in one underlying token.

### Call parameters

| Field            |        Type        | Description                                                                                                              |
| ---------------- | :----------------: | ------------------------------------------------------------------------------------------------------------------------ |
| pool\_id         |        `nat`       | pool identifier.                                                                                                         |
| shares           |        `nat`       | amount of LP tokens to be burnt.                                                                                         |
| token\_index     | `token_pool_idx_t` | index of token to be received.                                                                                           |
| min\_amount\_out |        `nat`       | amount of token to be received.                                                                                          |
| deadline         |     `timestamp`    | dealine of current operation.                                                                                            |
| receiver         |  `option(address)` | optional, address of the receiver of the LP tokens. If not provided the `sender` address will be used.                   |
| referral         |  `option(address)` | optional, address of the referral of the current operation. If not provided the `default_referral` address will be used. |

```pascaligo
type divest_one_c_param_t is [@layout:comb] record [
  pool_id                 : nat;
  shares                  : nat;
  token_index             : token_pool_idx_t;
  min_amount_out          : nat;
  deadline                : timestamp; 
  receiver                : option(address); 
  referral                : option(address);
]
```

{% hint style="danger" %}
The parameter `shares` provided to call, which represents the amount LP tokens would be burnt **in full**. So, if you want to burn more LP tokens **by value** than available reserves of the selected underlying token then you could **lose some of your liquidity**.
{% endhint %}
