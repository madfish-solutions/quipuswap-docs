---
description: Contract typings and storage
---

# 📄 Storage and types overview

### Base types

```pascaligo
type token_id_t        is nat

type pool_id_t         is nat

type token_pool_idx_t  is nat

type fa12_token_t      is address

type fa2_token_t       is [@layout:comb] record[ 
    token_address        : address; 
    token_id             : token_id_t; 
]

type token_t           is 
| Fa12                   of fa12_token_t 
| Fa2                    of fa2_token_t

type tokens_map_t      is map(nat, token_t);
```

### Staker accumulator - accumulator of QUIPU staking rewards.

| Field         |             Type             | Hint                                                            | Description                                                                      |
| ------------- | :--------------------------: | --------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| accumulator   | `map(token_pool_idx_t, nat)` | For better accuracy, stored with multiplication by $$10^{10}$$. | Mapping of token index and corresponding underlying accumulated balance of token |
| total\_staked |             `nat`            |                                                                 | balance of staked QUIPU tokens to current pool                                   |

```pascaligo
type staker_accum_t     is [@layout:comb] record [
  accumulator             : map(token_pool_idx_t, nat);
  total_staked            : nat;
]
```

### Fee storage - fee rates record

| Field   |  Type | Hint                                    | Description                                                                                                                                                                                                                |
| ------- | :---: | --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| lp      | `nat` | Float value. Multiplied by $$10^{10}$$. | <p>Percent of fee goes to liquidity providers.</p><p>This fee stays in liquidity pool to increase LP token price.</p>                                                                                                      |
| stakers | `nat` | Float value. Multiplied by $$10^{10}$$. | Percent of fee goes to QUIPU token stakers of pool. This fee goes to staking accumulator and spreads between users who staked QUIPU token to pool. If noone staked this fee part goes to liquidity pool as additional fee. |
| ref     | `nat` | Float value. Multiplied by $$10^{10}$$. | Percent of fee goes to referral of DEX call. This fee goes to referral address passed to DEX call. If referral not passed, fee goes to default referral.                                                                   |

```pascaligo
type fees_storage_t     is [@layout:comb] record [
  lp                      : nat;
  stakers                 : nat;
  ref                     : nat;
]
```

### Token information type - pool underlying token info

| Field                 |  Type | Hint                                                                                                                                           | Description                                                                                                    |
| --------------------- | :---: | ---------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| rate                  | `nat` | Calculates with pecisions. By default LP precision is 1e18. Rate is the value allowing to set custom exchange ratios between underlying tokens | Indicates how much LP token belongs to each underlying stablecoin                                              |
| precision\_multiplier | `nat` | By default LP precision is 1e18. Than `precision_multiplier` is $$10^{decimals_{LP} - decimals_{token}}$$__                                    | value that underlying token reserves are multiplied by in order to adjust their precision to LP decimal places |
| reserves              | `nat` |                                                                                                                                                | balance of underlying token, locked in pool                                                                    |

```pascaligo
type token_info_t       is  [@layout:comb] record [
  rate                    : nat;
  precision_multiplier    : nat;
  reserves                : nat;
]
```

### Pool type - DEX pool storage

| Field               |                  Type                 | Hint                                                                             | Description                                                                                                                                                   |
| ------------------- | :-----------------------------------: | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| initial\_A          |                 `nat`                 | A constant stores as multiplied value. $$A * n^{n-1} * 10^2$$(10^2 is precision) | Start value of ramping A contant.                                                                                                                             |
| initial\_A\_time    |              `timestamp`              | Timestamp in seconds                                                             | Time when ramping A constant was started.                                                                                                                     |
| future\_A           |                 `nat`                 | A constant stores as multiplied value. $$A * n^{n-1} * 10^2$$(10^2 is precision) | End value of ramping A contant.                                                                                                                               |
| future\_A\_time     |              `timestamp`              | Timestamp in seconds                                                             | Time when ramping A constant will be finished                                                                                                                 |
| tokens\_info        | `map(token_pool_idx_t, token_info_t)` |                                                                                  | [#token-information-type-pool-underlying-token-info](storage-and-types-overview.md#token-information-type-pool-underlying-token-info "mention")               |
| fee                 |            `fees_storage_t`           |                                                                                  | [#fee-storage-fee-rates-record](storage-and-types-overview.md#fee-storage-fee-rates-record "mention")                                                         |
| staker\_accumulator |            `staker_accum_t`           |                                                                                  | [#staker-accumulator-accumulator-of-quipu-staking-rewards.](storage-and-types-overview.md#staker-accumulator-accumulator-of-quipu-staking-rewards. "mention") |
| total\_supply       |                 `nat`                 |                                                                                  | Total supply of LP token.                                                                                                                                     |

```pascaligo
type pool_t             is [@layout:comb] record [
  initial_A               : nat;
  initial_A_time          : timestamp;
  future_A                : nat;
  future_A_time           : timestamp;
  tokens_info             : map(token_pool_idx_t, token_info_t);
  fee                     : fees_storage_t;
  staker_accumulator      : staker_accum_t;
  total_supply            : nat;
]
```

### Storage - main contract storage

| Field             |                                            Type                                           | Hint                                                                                         | Description                                                                                                                                  |
| ----------------- | :---------------------------------------------------------------------------------------: | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| admin             |                                         `address`                                         |                                                                                              | Administator of current contract                                                                                                             |
| default\_referral |                                         `address`                                         |                                                                                              | Default referral address to apply fees                                                                                                       |
| managers          |                                       `set(address)`                                      | Manager could edit LP token metadata.                                                        | Set of managers addresses                                                                                                                    |
| pools\_count      |                                           `nat`                                           | Counter. Always `1`                                                                          | Amount of pools created inside current contract.                                                                                             |
| tokens            |                             `big_map(pool_id_t, tokens_map_t)`                            |                                                                                              | Mapping of tokens, that exchanges inside created pool.                                                                                       |
| pool\_to\_id      |                                   `big_map(bytes, nat)`                                   | Bytes - packed by `Bytes.pack(tokens)` where tokens is valid `tokens_map_t` (sorted tokens). | Mapping that allows finding pool id by packed bytes of `tokens_map_t`                                                                        |
| pools             |                                `big_map(pool_id_t, pool_t)`                               |                                                                                              | Mapping of pool to it's corresponding pool [#pool-type-dex-pool-storage](storage-and-types-overview.md#pool-type-dex-pool-storage "mention") |
| ledger            |        <p><code>big_map(</code></p><p><code>(address * pool_id_t), nat)</code></p>        |                                                                                              | Mapping of user's LP token balance related to pool                                                                                           |
| allowances        | <p><code>big_map(</code></p><p><code>(address * pool_id_t), allowances_data_t)</code></p> |                                                                                              | Storage of operators allowed to transfer LP tokens of user's behalf.                                                                         |
| dev\_rewards      |                                  `big_map(token_t, nat)`                                  |                                                                                              | Mapping of accrued developer rewards by each token.                                                                                          |
| referral\_rewards |         <p><code>big_map(</code></p><p><code>(address * token_t), nat)</code></p>         |                                                                                              | Mapping of accrued referral rewards by each user-token key.                                                                                  |
| stakers\_balance  |   <p><code>big_map(</code></p><p><code>(address * pool_id_t), staker_info_t)</code></p>   |                                                                                              | Mapping of accrued staking rewards by each user-token key.                                                                                   |
| quipu\_token      |                                       `fa2_token_t`                                       |                                                                                              | QUIPU token address and token ID                                                                                                             |
| started           |                                           `bool`                                          | [freeze.md](initialization/freeze.md "mention")                                              | flag that used in initialization stage                                                                                                       |
| factory\_address  |                                         `address`                                         | this field setted at deploy and has no methods for changing                                  | address of factory                                                                                                                           |

```pascaligo
type storage_t          is [@layout:comb] record [
  (* Management *)
  admin                   : address;
  default_referral        : address;
  managers                : set(address);

  (* Pools data *)
  pools_count             : nat; (* total pools count *)
  tokens                  : big_map(pool_id_t, tokens_map_t); (* all the tokens list *)
  pool_to_id              : big_map(bytes, nat); (* all the tokens list *)
  pools                   : big_map(pool_id_t, pool_t); (* pool info per token id *)

  (* FA2 data *)
  ledger                  : big_map((address * pool_id_t), nat); (* account info per address *)
  allowances              : big_map((address * pool_id_t), allowances_data_t); (* account info per each lp provider *)

  (* Rewards and accumulators *)
  dev_rewards             : big_map(token_t, nat);
  referral_rewards        : big_map((address * token_t), nat);
  stakers_balance         : big_map((address * pool_id_t), staker_info_t);
  quipu_token             : fa2_token_t;
  (* dev storage params *)
  dev_store               : dev_storage_t;
]
```

### Full storage type - storage root

| Field           |                   Type                   | Hint                                                                                                    | Description                                                                                                         |
| --------------- | :--------------------------------------: | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| storage         |                `storage_t`               | [#storage-main-contract-storage](storage-and-types-overview.md#storage-main-contract-storage "mention") | Indicates how much LP token belongs to each underlying stablecoin                                                   |
| metadata        |         `big_map(string, bytes)`         | TZIP-016                                                                                                | contract metadata by [TZIP-016](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-16/tzip-16.md)           |
| token\_metadata | `big_map(token_id_t, token_meta_info_t)` | TZIP-016, TZIP-012                                                                                      | mapping each token metadata by [TZIP-012](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md) |
| admin\_lambdas  |           `big_map(nat, bytes)`          |                                                                                                         | Administrative lambda-methods storage                                                                               |
| dex\_lambdas    |           `big_map(nat, bytes)`          |                                                                                                         | DEX stable swap protocol lambda-methods storage                                                                     |
| token\_lambdas  |           `big_map(nat, bytes)`          |                                                                                                         | FA2 lambda-methods storage                                                                                          |

```pascaligo
type full_storage_t     is [@layout:comb] record [
  storage                 : storage_t; (* real dex storage_t *)
  (* Token Metadata *)
  metadata                : big_map(string, bytes); (* metadata storage_t according to TZIP-016 *)
  token_metadata          : big_map(token_id_t, token_meta_info_t);
  (* Contract lambdas storage *)
  admin_lambdas           : big_map(nat, bytes); (* map with admin-related functions code *)
  dex_lambdas             : big_map(nat, bytes); (* map with exchange-related functions code *)
  token_lambdas           : big_map(nat, bytes); (* map with token-related functions code *)
]
```
