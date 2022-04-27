# flash\_swap\_callback

An entrypoint that executes after execution of user's lambda but only in case when user is trying to loan TEZ tokens. It checks the returns of TEZ tokens and [**fills**](../../../bucket-contract/entrypoints-overview/fill.md) it to the appropriative [Bucket](../../../bucket-contract/) contract.

When user need to return TEZ tokens, he need to transfer correct amount of TEZ tokens to the [DexCore](../../) contract at the end of his lambda execution.

### Call parameters

```pascaligo
type token_id_t         is nat

type flash_swap_1_t     is [@layout:comb] record [
  pair_id                 : token_id_t;
  prev_tez_balance        : nat;
  amount_in               : nat;
]
```

| Field              | Type               | Description                                                                 |
| ------------------ | ------------------ | --------------------------------------------------------------------------- |
| pair\_id           | token\_id\_t (nat) | Identifier of the liquidity pool (pair)                                     |
| prev\_tez\_balance | nat                | TEZ balance of [DexCore](../../) contract before execution of user's lambda |
| amount\_in         | nat                | The number of incoming tokens (amount that user must repay)                 |

### Usage

Only [DexCore](../../) contract can call this entrypoint.

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `113` - a [Bucket](../../../bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `129` - wrong amount of flash swap returns.
* `138` - only entered (transaction must be not the first transaction in the chain of calls).
* `403` - `sender` of the transaction is not [DexCore](../../) contract.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
