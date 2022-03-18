# stake

This entrypoint is designed to stake or unstake QUIPU tokens to a specific DEX pool.

{% hint style="info" %}
This call payoff staking rewards in all accrued tokens automatically.

Calling this method with `amount = 0n` and any path (`Add/Remove`) triggers payoff without transfer QUIPU tokens.&#x20;
{% endhint %}

### Call parameters

| Field    |     Type    | Description                                 |
| -------- | :---------: | ------------------------------------------- |
| pool\_id | `pool_id_t` | pool identifier.                            |
| amount   |    `nat`    | amount of QUIPU tokens to stake or unstake. |

```pascaligo
type stake_param_t      is [@layout:comb] record [
  pool_id                 : pool_id_t;
  amount                  : nat;

type stake_action_t     is
| Add of stake_param_t
| Remove of stake_param_t
```
