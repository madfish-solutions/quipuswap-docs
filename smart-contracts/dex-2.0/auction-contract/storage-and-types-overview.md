# Storage and types overview

### token\_t

```pascaligo
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

### status\_auction\_t

```pascaligo
type status_auction_t   is
| Active                  of unit
| Finished                of unit
```

### auction\_t

| Field           | Type                                                                   | Description                                         |
| --------------- | ---------------------------------------------------------------------- | --------------------------------------------------- |
| status          | [status\_auction\_t](storage-and-types-overview.md#status\_auction\_t) | Status of auction                                   |
| token           | [token\_t](storage-and-types-overview.md#token\_t)                     | FA1.2/FA2/TEZ token                                 |
| end\_time       | timestamp                                                              | Time when auction will be finished                  |
| current\_bidder | address                                                                | Address of a user who made current bid              |
| current\_bid    | nat                                                                    | Current bid                                         |
| amt             | nat                                                                    | Amount of tokens that that were put up for auction  |

```pascaligo
type auction_t          is [@layout:comb] record [
  status                  : status_auction_t;
  token                   : token_t;
  end_time                : timestamp;
  current_bidder          : address;
  current_bid             : nat;
  amt                     : nat;
]
```

### fees\_t

| Field       | Type | Hint                            | Description                                                                                                                                     |
| ----------- | ---- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| dev\_fee\_f | nat  | Float value multiplied by 1e+18 | Fee that goes to the devs fund and can be [withdrawn](entrypoints-overview/admin-entrypoints/withdraw\_dev\_fee.md) by an administrator         |
| bid\_fee\_f | nat  | Float value multiplied by 1e+18 | Fee in [QuipuSwap Governance token](https://tzkt.io/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/operations/) that applies on each bid for all auctions |

```pascaligo
type fees_t             is [@layout:comb] record [
  dev_fee_f               : nat;
  bid_fee_f               : nat;
]
```

### storage\_t - main contract storage

| Field                    | Type                                                                  | Hint                            | Description                                                                                                                                                                                                                                        |
| ------------------------ | --------------------------------------------------------------------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| auctions                 | big\_map(nat, [auction\_t](storage-and-types-overview.md#auction\_t)) |                                 | Mapping of auction IDs' to auctions                                                                                                                                                                                                                |
| dev\_fee\_balances\_f    | big\_map([token\_t](storage-and-types-overview.md#token\_t), nat)     | Float value multiplied by 1e+18 | Mapping of tokens to their balances that can be [withdrawn](entrypoints-overview/admin-entrypoints/withdraw\_dev\_fee.md) by an administrator                                                                                                      |
| public\_fee\_balances\_f | big\_map([token\_t](storage-and-types-overview.md#token\_t), nat)     | Float value multiplied by 1e+18 | Mapping of tokens to their balances for which auction can be launched (except of whitelisted tokens)                                                                                                                                               |
| whitelist                | set([token\_t](storage-and-types-overview.md#token\_t))               |                                 | A set of tokens for which an auction can't be started. Can be [updated](entrypoints-overview/admin-entrypoints/update\_whitelist.md) by an administrator                                                                                           |
| quipu\_token             | [fa2\_token\_t](storage-and-types-overview.md#token\_t)               |                                 | [QuipuSwap Governance token](https://tzkt.io/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/operations/) address and ID                                                                                                                                      |
| fees                     | [fees\_t](storage-and-types-overview.md#fees\_t)                      |                                 | Fees that applies to each received token                                                                                                                                                                                                           |
| baker                    | option(key\_hash)                                                     |                                 | Baker for whom all TEZ tokens on the contract were delegated. Can be [changed](entrypoints-overview/admin-entrypoints/set\_baker.md) by an administrator                                                                                           |
| admin                    | address                                                               |                                 | Administrator of the contract                                                                                                                                                                                                                      |
| pending\_admin           | option(address)                                                       |                                 | Pending administrator that should accept his new administrator role (if he is not `None`)                                                                                                                                                          |
| dex\_core                | address                                                               |                                 | [DexCore](../dexcore-contract/) contract address                                                                                                                                                                                                   |
| bid\_fee\_balance\_f     | nat                                                                   | Float value multiplied by 1e+18 | Bid fee balance in [QuipuSwap Governance token](https://tzkt.io/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/operations/) that were withdrawn from each bid. Can be [burned](entrypoints-overview/admin-entrypoints/burn\_bid\_fee.md) by an administrator |
| auctions\_count          | nat                                                                   |                                 | Number of auctions created by all users                                                                                                                                                                                                            |
| auction\_duration        | nat                                                                   |                                 | Duration of each auction that will be created. Can be [changed](entrypoints-overview/admin-entrypoints/set\_auction\_duration.md) by an administrator                                                                                              |
| min\_bid                 | nat                                                                   |                                 | Minimum possible bid in time of auction launch. Can be [changed](entrypoints-overview/admin-entrypoints/set\_min\_bid.md) by an administrator                                                                                                      |

```pascaligo
type storage_t          is [@layout:comb] record [
  auctions                : big_map(nat, auction_t);
  dev_fee_balances_f      : big_map(token_t, nat);
  public_fee_balances_f   : big_map(token_t, nat);
  whitelist               : set(token_t);
  quipu_token             : fa2_token_t;
  fees                    : fees_t;
  baker                   : option(key_hash);
  admin                   : address;
  pending_admin           : option(address);
  dex_core                : address;
  bid_fee_balance_f       : nat;
  auctions_count          : nat;
  auction_duration        : int;
  min_bid                 : nat;
]
```

### full\_storage\_t - storage root

| Field            | Type                                                                         | Description                                                                                                           |
| ---------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| storage          | [storage\_t](storage-and-types-overview.md#storage\_t-main-contract-storage) | Actual storage of the contract                                                                                        |
| auction\_lambdas | big\_map(nat, bytes)                                                         | Contract's lambda-methods                                                                                             |
| metadata         | big\_map(string, bytes)                                                      | Contract's metadata according to [TZIP-016](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-16/tzip-16.md) |

```pascaligo
type full_storage_t     is [@layout:comb] record [
  storage                 : storage_t;
  auction_lambdas         : big_map(nat, bytes);
  metadata                : big_map(string, bytes);
]
```
