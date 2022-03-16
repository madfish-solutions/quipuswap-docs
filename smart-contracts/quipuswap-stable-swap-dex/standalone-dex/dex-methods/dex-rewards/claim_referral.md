# claim\_referral

This entrypoint is designed to withdraw some of the collected referral rewards by the selected token.

### Call params

```pascaligo
type claim_by_token_param_t is [@layout:comb] record [
  token                   : token_t;
  (* FA12/FA2 token to withdraw *)
  amount                  : nat;
  (* amount of tokens to withdraw *)
]
```
