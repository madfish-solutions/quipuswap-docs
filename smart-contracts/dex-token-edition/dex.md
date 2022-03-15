# Dex

The contract is responsible for launching new exchange pairs and serves as the automatic market maker engine. The contract manages pools for FA1.2/FA1.2, FA2/FA2 and FA2/FA1.2 tokens. The only instance of the pool for the same pair exists.

The contract fully implements the entrypoints of the FA2 standard according to [TZIP-12](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md). The other exchange-specific entrypoints are described in the doc.

## Code

{% embed url="https://github.com/madfish-solutions/quipuswap-token2token-core/blob/master/contracts/main/Dex.ligo" %}

## State-Changing Functions

### AddPair

{% code title="types.ligo" %}
```
type fa2_token_type     is
record [
  token_address           : address;
  token_id                : nat;
]

type token_type        is
| Fa12                    of address
| Fa2                     of fa2_token_type


type tokens_type        is 
[@layout:comb]
record [
  token_a_type            : token_type; (* token A standard *)
  token_b_type            : token_type; (* token B standard *)
]


type add_pair_params  is 
[@layout:comb]
record [
  pair                    : tokens_type; (* exchange pair info *)
  token_a_in              : nat; (* min amount of tokens A invested  *)
  token_b_in              : nat; (* min amount of tokens B invested *)
]
```
{% endcode %}

Setup the new exchange or relaunch the exchange after all the liquidity was drained. `amount_a_in` and `amount_b_in` of tokens must be approved. Initial liquidity should be non-zero. All the storage parameters are reset to default values. The sender receives shares equal to a minimum of `amount_a_in` and `amount_b_in`. Tokens types must be provided in ascending order.

| Parameter        | Type         | Description                               |
| ---------------- | ------------ | ----------------------------------------- |
| token\_a\_type   | tokens\_type | The type of the first token               |
| token\_b\_type   | tokens\_type | The type of the second token              |
| token\_a\_in     | nat          | Amount of the first token to be invested  |
| token\_b\_in     | nat          | Amount of the second token to be invested |

### Swap

```
type swap_type          is
| A_to_b
| B_to_a

type swap_slice_type    is 
record [
  pair_id                 : nat;
  operation               : swap_type;
]

type swap_type          is 
[@layout:comb]
record [
  swaps                   : list(swap_slice_type);
  amount_in               : nat;
  min_amount_out          : nat;
  receiver                : address;
  deadline                : timestamp;
]
 
```

Swaps the token to another token. `a_to_b` type is used to exchange `token_a` to `token_b`. `b_to_a` performs the opposite swap from `token_b_address` to `token_a_address`. The `token_a` and `token_b`  are the corresponding tokens of `pair_id` pool. The `amount_in` of the token will be charged from the user. If the received amount is smaller than `min_amount_out` then the transaction is reverted. Tokens types must be provided in ascending order. Deadlines should be in the future.&#x20;

| Parameter        | Type                      | Description                                                                                                                          |
| ---------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| swaps            | list of swap\_slice\_type | Swaps to perform; each swap consist of `pair_id` of the pool and `swap_type` to be executed; all the exchanges should be sequential. |
| amount\_in       | nat                       | Amount of the token to swap                                                                                                          |
| min\_amount\_out | nat                       | The minimal amount of the token to receive                                                                                           |
| receiver         | address                   | Receiver's address                                                                                                                   |
| deadline         | timestamp                 | Time until the operation is valid                                                                                                    |

### Invest

```
type invest_type        is 
[@layout:comb]
record [
  pair_id                 : nat;
  shares                  : nat;
  token_a_in              : nat;
  token_b_in              : nat;
  deadline                : timestamp;
]

```

Adds more liquidity to the exchange. `token_a_in` and `token_b_in` must be approved. Initial liquidity should be non-zero. The sender spends `token_a_in` and `token_b_in` at most otherwise, the transaction fails. Tokens types must be provided in ascending order. Deadlines should be in the future.&#x20;

| Parameter    | Type      | Description                              |
| ------------ | --------- | ---------------------------------------- |
| pair\_id     | nat       | Pair identifier                          |
| shares       | nat       | Amount of LP tokens to mint              |
| token\_a\_in | nat       | Max amount of the first token to invest  |
| token\_b\_in | nat       | Max amount of the second token to invest |
| deadline     | timestamp | Time until the operation is valid        |

### Divest

```
type divest_type        is 
[@layout:comb]
record [
  pair_id                 : nat;
  min_token_a_out         : nat;
  min_token_b_out         : nat;
  shares                  : nat;
  deadline                : timestamp;
]
```

Burns `shares` and sends tokens to the owner; operation is reverted if the amount of appropriate divested tokens is smaller than `min_token_a_out` or `min_token_b_out`. Tokens types must be provided in ascending order. Deadlines should be in the future.&#x20;

| Parameter          | Type      | Description                                   |
| ------------------ | --------- | --------------------------------------------- |
| pair\_id           | nat       | Pair identifier                               |
| min\_token\_a\_out | nat       | Minimal amount of the first token to receive  |
| min\_token\_b\_out | nat       | Minimal amount of the second token to receive |
| shares             | nat       | The amount of the shares to burn              |
| deadline           | timestamp | Time until the operation is valid             |

### Close

```
type close_type        is unit
```

Is used after all the exchange calls to prevent reentrancy. It can only be called by the exchange itself.&#x20;

## Read-Only Functions

### Get\_reserves&#x20;

```
type reserves_type      is 
record [
  receiver                : contract(nat * nat);
  pair_id                 : nat;
]
```

Returns the amount of tokens reserves. No arguments are needed.

