# Storage and types overview

### token\_t

```pascaligo
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
```

### token\_metadata\_t

| Field       | Type                                                   | Description                             |
| ----------- | ------------------------------------------------------ | --------------------------------------- |
| token\_id   | [token\_id\_t](storage-and-types-overview.md#token\_t) | Token's ID                              |
| token\_info | map(string, bytes)                                     | Mapping of token's keys to token's info |

```pascaligo
type token_metadata_t   is [@layout:comb] record [
  token_id                : token_id_t;
  token_info              : map(string, bytes);
]
```

### account\_t

| Field      | Type         | Description                                       |
| ---------- | ------------ | ------------------------------------------------- |
| allowances | set(address) | Set of accounts who can transfer user's LP tokens |

```pascaligo
type account_t          is [@layout:comb] record [
  allowances              : set(address);
]
```

### tokens\_t

| Field    | Type                                               | Description |
| -------- | -------------------------------------------------- | ----------- |
| token\_a | [token\_t](storage-and-types-overview.md#token\_t) | Token A     |
| token\_b | [token\_t](storage-and-types-overview.md#token\_t) | Token B     |

```pascaligo
type tokens_t           is [@layout:comb] record [
  token_a                 : token_t;
  token_b                 : token_t;
]
```

### pair\_t

| Field                  | Type            | Description                                                                |
| ---------------------- | --------------- | -------------------------------------------------------------------------- |
| token\_a\_pool         | nat             | Supply of token A in the pool                                              |
| token\_b\_pool         | nat             | Supply of token B in the pool                                              |
| token\_a\_price\_cml   | nat             | Cumulative price of token A                                                |
| token\_b\_price\_cml   | nat             | Cumulative price of token B                                                |
| total\_supply          | nat             | Total supply of LP token                                                   |
| last\_block\_timestamp | timestamp       | Timestamp of the last block that is used for cumulative prices calculation |
| bucket                 | option(address) | [Bucket](../bucket-contract/) contract address (only for TOK/TEZ pools)    |

```pascaligo
type pair_t             is [@layout:comb] record [
  token_a_pool            : nat;
  token_b_pool            : nat;
  token_a_price_cml       : nat;
  token_b_price_cml       : nat;
  total_supply            : nat;
  last_block_timestamp    : timestamp;
  bucket                  : option(address);
]
```

### permit\_info\_t

| Field       | Type               | Description                                                                                                                         |
| ----------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| created\_at | timestamp          | Timestamp of permit creation                                                                                                        |
| expiry      | option(seconds\_t) | Permit's default expiry (see [TZIP-017](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-17/tzip-17.md) for more details) |

```pascaligo
type permit_info_t      is [@layout:comb] record [
  created_at              : timestamp;
  expiry                  : option(seconds_t);
]
```

### user\_permit\_t

| Field   | Type                                                                                    | Description                                                                                                                               |
| ------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| permits | map(blake2b\_hash\_t, [permit\_info\_t](storage-and-types-overview.md#permit\_info\_t)) | Mapping of permits' hashes (bytes) to their info                                                                                          |
| expiry  | option(seconds\_t)                                                                      | User's permits default expiry (see [TZIP-017](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-17/tzip-17.md) for more details) |

```pascaligo
type user_permits_t     is [@layout:comb] record [
  permits                 : map(blake2b_hash_t, permit_info_t);
  expiry                  : option(seconds_t);
]
```

### fees\_t

| Field                 | Type | Hint                            | Description                                                                                                                                                                                     |
| --------------------- | ---- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| interface\_fee        | nat  | Float value multiplied by 1e+18 | Fee that goes to referrers or UI/UX providers charged from exchanged amount                                                                                                                     |
| swap\_fee             | nat  | Float value multiplied by 1e+18 | Fee charged from exchanged amount that goes to the liquidity pool (for liquidity providers)                                                                                                     |
| auction\_fee          | nat  | Float value multiplied by 1e+18 | Fee charged from exchanged amount that goes to the [Auction](../auction-contract/) contract                                                                                                     |
| withdraw\_fee\_reward | nat  | Float value multiplied by 1e+18 | The % of the rewards that will be transferred to the transaction sender when he calls [_**withdraw\_auction\_fee**_](entrypoints-overview/dex-entrypoints/withdraw\_auction\_fee.md) entrypoint |

```pascaligo
type fees_t             is [@layout:comb] record [
  interface_fee           : nat;
  swap_fee                : nat;
  auction_fee             : nat;
  withdraw_fee_reward     : nat;
]
```

### storage\_t - main contract storage

| Field               | Type                                                                                                                                     | Description                                                                                                                                                                                                                                        |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| token\_metadata     | big\_map([token\_id\_t](storage-and-types-overview.md#token\_t), [token\_metadata\_t](storage-and-types-overview.md#token\_metadata\_t)) | Mapping of pools' IDs to their metadata                                                                                                                                                                                                            |
| ledger              | big\_map((address \* [token\_id\_t](storage-and-types-overview.md#token\_t)), nat)                                                       | Mapping of accounts' addresses and pools' IDs to their LP tokens' balances                                                                                                                                                                         |
| accounts            | big\_map((address \* [token\_id\_t](storage-and-types-overview.md#token\_t)), [account\_t](storage-and-types-overview.md#account\_t))    | Mapping of accounts' addresses and pools' IDs to their accounts                                                                                                                                                                                    |
| tokens              | big\_map([token\_id\_t](storage-and-types-overview.md#token\_t), [tokens\_t](storage-and-types-overview.md#tokens\_t))                   | Mapping of pools' IDs to their tokens                                                                                                                                                                                                              |
| token\_to\_id       | big\_map(bytes, [token\_id\_t](storage-and-types-overview.md#token\_t))                                                                  | Mapping of tokens (packed to bytes) to their pool IDs                                                                                                                                                                                              |
| pairs               | big\_map([token\_id\_t](storage-and-types-overview.md#token\_t), [pair\_t](storage-and-types-overview.md#pair\_t))                       | Mapping of tokens' IDs to information about the pools of these tokens                                                                                                                                                                              |
| permits             | big\_map(address, [user\_permits\_t](storage-and-types-overview.md#user\_permit\_t))                                                     | Mapping of accounts to created by them permits (see [TZIP-017](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-17/tzip-17.md) for more details)                                                                                         |
| interface\_fee      | big\_map(([token\_t](storage-and-types-overview.md#token\_t) \* address), nat)                                                           | Mapping of FA1.2/FA2 tokens and referrers or UI/UX providers to their fees balances in these tokens                                                                                                                                                |
| interface\_tez\_fee | big\_map(([token\_id\_t](storage-and-types-overview.md#token\_t) \* address), nat)                                                       | Mapping of pair IDs and referrers or UI/UX providers to their fees balances in TEZ tokens                                                                                                                                                          |
| auction\_fee        | big\_map([token\_t](storage-and-types-overview.md#token\_t), nat)                                                                        | Mapping of FA1.2/FA2 tokens to their fees balances in these tokens that will go to the [Auction](../auction-contract/) contract                                                                                                                    |
| auction\_tez\_fee   | big\_map([token\_id\_t](storage-and-types-overview.md#token\_t), nat)                                                                    | Mapping of pair IDs to their fees balances in TEZ tokens that will go to the [Auction](../auction-contract/) contract                                                                                                                              |
| managers            | set(address)                                                                                                                             | A set of addresses who can update tokens metadata. Can be [updated](entrypoints-overview/admin-entrypoints/add\_managers.md) by an administrator                                                                                                   |
| fees                | [fees\_t](storage-and-types-overview.md#fees\_t)                                                                                         | Fees that applies during each [_**swap**_](entrypoints-overview/dex-entrypoints/swap.md) or [_**flash\_swap**_](entrypoints-overview/dex-entrypoints/swap.md) _****_ operation                                                                     |
| admin               | address                                                                                                                                  | Administrator of the contract                                                                                                                                                                                                                      |
| pending\_admin      | option(address)                                                                                                                          | Pending administrator that should accept his new administrator role (if he is not `None`)                                                                                                                                                          |
| baker\_registry     | address                                                                                                                                  | [BakerRegistry](../bakerregistry-contract/) contract address                                                                                                                                                                                       |
| flash\_swaps\_proxy | address                                                                                                                                  | [FlashSwapsProxy](../flashswapsproxy-contract/) contract address. Can be [changed](entrypoints-overview/admin-entrypoints/set\_flash\_swaps\_proxy.md) by an administrator                                                                         |
| auction             | address                                                                                                                                  | [Auction](../auction-contract/) contract address. Can be [changed](entrypoints-overview/admin-entrypoints/set\_auction.md) by an administrator                                                                                                     |
| permits\_counter    | counter\_t (nat)                                                                                                                         | Number of permits created in this contract                                                                                                                                                                                                         |
| default\_expiry     | seconds\_t (nat)                                                                                                                         | Permits default expiry (see [TZIP-017](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-17/tzip-17.md) for more details)                                                                                                                 |
| entered             | bool                                                                                                                                     | Indicator that helps to avoid reentrancy                                                                                                                                                                                                           |
| tokens\_count       | nat                                                                                                                                      | Number of exchanges (pairs) launched in this contract                                                                                                                                                                                              |
| collecting\_period  | nat                                                                                                                                      | Period in blocks during which bakers' rewards are collected and not distributed between voters in [Bucket](../bucket-contract/) contracts. Can be [changed](entrypoints-overview/admin-entrypoints/set\_collecting\_period.md) by an administrator |

```pascaligo
type storage_t          is [@layout:comb] record [
  token_metadata          : big_map(token_id_t, token_metadata_t);
  ledger                  : big_map((address * token_id_t), nat);
  accounts                : big_map((address * token_id_t), account_t);
  tokens                  : big_map(token_id_t, tokens_t);
  token_to_id             : big_map(bytes, token_id_t);
  pairs                   : big_map(token_id_t, pair_t);
  permits                 : big_map(address, user_permits_t);
  interface_fee           : big_map((token_t * address), nat);
  interface_tez_fee       : big_map((token_id_t * address), nat);
  auction_fee             : big_map(token_t, nat);
  auction_tez_fee         : big_map(token_id_t, nat);
  managers                : set(address);
  fees                    : fees_t;
  admin                   : address;
  pending_admin           : option(address);
  baker_registry          : address;
  flash_swaps_proxy       : address;
  auction                 : address;
  permits_counter         : counter_t;
  default_expiry          : seconds_t;
  entered                 : bool;
  tokens_count            : nat;
  collecting_period       : nat;
]
```

### full\_storage\_t - storage root

| Field              | Type                                                                         | Description                                                                                                           |
| ------------------ | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| storage            | [storage\_t](storage-and-types-overview.md#storage\_t-main-contract-storage) | Actual storage of the contract                                                                                        |
| dex\_core\_lambdas | big\_map(nat, bytes)                                                         | Contract's lambda-methods                                                                                             |
| metadata           | big\_map(string, bytes)                                                      | Contract's metadata according to [TZIP-016](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-16/tzip-16.md) |

```pascaligo
type full_storage_t     is [@layout:comb] record [
  storage                 : storage_t;
  dex_core_lambdas        : big_map(nat, bytes);
  metadata                : big_map(string, bytes);
]
```
