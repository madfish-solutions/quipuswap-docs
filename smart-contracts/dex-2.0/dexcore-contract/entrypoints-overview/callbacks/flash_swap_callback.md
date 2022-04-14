# flash\_swap\_callback

An entrypoint that executes after execution of user's lambda. It calculates the returns, checks all additional data and transfers needed amount of tokens from user.

When user need to return TEZ tokens, he need to transfer correct amount of TEZ tokens to the [DexCore](../../) contract at the end of his lambda execution.

### Call parameters

```pascaligo
type flash_swap_rule_t  is
| Loan_a_return_a
| Loan_a_return_b
| Loan_b_return_a
| Loan_b_return_b

type token_id_t         is nat

type tez_t              is unit

type fa12_token_t       is address

type fa2_token_t        is [@layout:comb] record [
  token                   : address;
  id                      : nat;
]

type token_t            is
| Tez                     of tez_t
| Fa12                    of fa12_token_t
| Fa2                     of fa2_token_t

type flash_swap_1_t     is [@layout:comb] record [
  flash_swap_rule         : flash_swap_rule_t;
  pair_id                 : token_id_t;
  return_token            : token_t;
  referrer                : address;
  sender                  : address;
  swap_token_pool         : nat;
  return_token_pool       : nat;
  amount_out              : nat;
  prev_tez_balance        : nat;
]
```

| Field               | Type                 | Description                                                                 |
| ------------------- | -------------------- | --------------------------------------------------------------------------- |
| flash\_swap\_rule   | flash\_swap\_rule\_t | Rule of a flash swap (which token to take and which token to return)        |
| pair\_id            | token\_id\_t (nat)   | Identifier of the liquidity pool (pair)                                     |
| return\_token       | token\_t             | FA1.2/FA2/TEZ token                                                         |
| referrer            | address              | Referrer to whom interface fee will be paid                                 |
| sender              | address              | Sender of _**flash\_swap**_ transaction                                     |
| swap\_token\_pool   | nat                  | Pool of the swap token                                                      |
| return\_token\_pool | nat                  | Pool of the return token                                                    |
| amount\_out         | nat                  | The number of outgoing tokens                                               |
| prev\_tez\_balance  | nat                  | TEZ balance of [DexCore](../../) contract before execution of user's lambda |

### Usage

Only [DexCore](../../) contract can call this entrypoint.

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `113` - a [Bucket](../../../bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `129` - wrong amount of flash swap returns.
* `138` - only entered (transaction must be not the first transaction in the chain of calls).
* `403` - `sender` of the transaction is not [DexCore](../../) contract.
