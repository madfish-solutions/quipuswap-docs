# claim\_referral

This entrypoint is designed to withdraw some of the collected referral rewards by the selected token.

### Call parameters

| Field  |    Type   | Description                 |
| ------ | :-------: | --------------------------- |
| token  | `token_t` | `FA2/FA1.2` token to claim. |
| amount |   `nat`   | amount of tokens to claim.  |

```pascaligo
type claim_by_token_param_t is [@layout:comb] record [
  token                   : token_t;
  amount                  : nat;
]
```
