# Storage and types overview

### token\_type

```pascaligo
type fa12_type          is address

type fa2_type           is [@layout:comb] record [
  token                   : address;
  id                      : token_id_type;
]

type token_type         is
  FA12                    of fa12_type
| FA2                     of fa2_type
```

### fees\_type

| Field           | Type | Hint                            | Description                                                                                                                      |
| --------------- | ---- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| harvest\_fee    | nat  | Float value multiplied by 1e+16 | Fee that applies in time of rewards claiming                                                                                     |
| withdrawal\_fee | nat  | Float value multiplied by 1e+16 | Fee that applies in time of withdrawing (unstaking) tokens only in farms with timelock. Applies only in case of early withdrawal |

```pascaligo
type fees_type          is [@layout:comb] record [
  harvest_fee             : nat;
  withdrawal_fee          : nat;
]
```

### stake\_params\_type

| Field         | Type                                                     | Description                                              |
| ------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| staked\_token | [token\_type](storage-and-types-overview.md#token\_type) | FA1.2/FA2 staked token                                   |
| is\_v1\_lp    | bool                                                     | Flag that indicates: QuipuSwap V1 LP token staked or not |

```pascaligo
w
```

### farm\_type

| Field               | Type                                                                     | Description                                            |
| ------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------ |
| fees                | [fees\_type](storage-and-types-overview.md#fees\_type)                   | Fees that applies to the farming                       |
| upd                 | timestamp                                                                | Last time of farm's rewards updating                   |
| stake\_params       | [stake\_params\_type](storage-and-types-overview.md#stake\_params\_type) | Staking parameters                                     |
| reward\_token       | [token\_type](storage-and-types-overview.md#token\_type)                 | FA1.2/FA2 token                                        |
| timelock            | nat                                                                      | Timelock in seconds (0 for farms without timelock)     |
| current\_delegated  | key\_hash                                                                | A baker account TEZ tokens are currently delegated for |
| next\_candidate     | key\_hash                                                                | A best candidate to become current delegated           |
| paused              | bool                                                                     | Flag that indicates: farm is paused or not             |
| reward\_per\_second | nat                                                                      | Reward per second                                      |
| reward\_per\_share  | nat                                                                      | Accumulator for reward per 1 staked token's unit       |
| staked              | nat                                                                      | Total count of staked tokens in farm                   |
| claimed             | nat                                                                      | Total count of claimed tokens                          |
| start\_time         | timestamp                                                                | Farm's start time                                      |
| end\_time           | timestamp                                                                | Farm's end time                                        |
| fid                 | fid\_type (nat)                                                          | Farm's ID                                              |

```pascaligo
type farm_type          is [@layout:comb] record [
  fees                    : fees_type;
  upd                     : timestamp;
  stake_params            : stake_params_type;
  reward_token            : token_type;
  timelock                : nat;
  current_delegated       : key_hash;
  next_candidate          : key_hash;
  paused                  : bool;
  reward_per_second       : nat;
  reward_per_share        : nat;
  staked                  : nat;
  claimed                 : nat;
  start_time              : timestamp;
  end_time                : timestamp;
  fid                     : fid_type;
]
```

### user\_info\_type

| Field        | Type         | Description                                                     |
| ------------ | ------------ | --------------------------------------------------------------- |
| last\_staked | timestamp    | Last time when user staked tokens                               |
| staked       | nat          | Total amount of tokens staked by user                           |
| earned       | nat          | Amount of tokens earned by user                                 |
| claimed      | nat          | A mount of tokens claimed by user per all time                  |
| prev\_earned | nat          | Amount of tokens staked by user multiplied by rewards per share |
| prev\_staked | nat          | Total amount of tokens staked by user in previous contract call |
| allowances   | set(address) | Set of user's allowances for staked tokens transfer             |

```pascaligo
type user_info_type     is [@layout:comb] record [
  last_staked             : timestamp;
  staked                  : nat;
  earned                  : nat;
  claimed                 : nat;
  prev_earned             : nat;
  prev_staked             : nat;
  allowances              : set(address);
]
```

### baker\_type

| Field  | Type      | Description                                           |
| ------ | --------- | ----------------------------------------------------- |
| period | nat       | Period during which baker will be banned (in seconds) |
| start  | timestamp | Ban start time                                        |

```pascaligo
type baker_type         is [@layout:comb] record [
  period                  : nat;
  start                   : timestamp;
]
```

### tok\_meta\_type

| Field       | Type               | Description                             |
| ----------- | ------------------ | --------------------------------------- |
| token\_id   | nat                | Token ID                                |
| token\_info | map(string, bytes) | Mapping of token's keys to token's info |

```pascaligo
type tok_meta_type      is [@layout:comb] record [
  token_id                : nat;
  token_info              : map(string, bytes);
]
```

### storage\_type - main contract storage

| Field           | Type                                                                                                 | Description                                                                                                                  |
| --------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| farms           | big\_map(fid\_type, [farm\_type](storage-and-types-overview.md#farm\_type))                          | Mapping of all farmings on the contract                                                                                      |
| referrers       | big\_map(address, address)                                                                           | Mapping of users' addresses to their referrers' addresses                                                                    |
| users\_info     | big\_map((fid\_type \* address), [user\_info\_type](storage-and-types-overview.md#user\_info\_type)) | Mapping of farms' IDs and users' addresses  (in pair) to users' info                                                         |
| votes           | big\_map((fid\_type \* key\_hash), nat)                                                              | Mapping of farms' IDs and bakers' addresses (in pair) to votes for this bakers                                               |
| candidates      | big\_map((fid\_type \* address), key\_hash)                                                          | Mapping of farms' IDs and users' addresses (in pair) to users' candidates in voting                                          |
| banned\_bakers  | big\_map(key\_hash, [baker\_type](storage-and-types-overview.md#baker\_type))                        | Mapping of banned bakers' addresses to their ban info                                                                        |
| token\_metadata | big\_map(fid\_type, [tok\_meta\_type](storage-and-types-overview.md#tok\_meta\_type))                | Mapping of tokens' IDs to tokens' metadata                                                                                   |
| qsgov           | fa2\_type                                                                                            | QuipuSwap Governance token info (address and token ID)                                                                       |
| qsgov\_lp       | address                                                                                              | Address of the [QUIPU/TEZ LP token ](https://quipuswap.com/swap/tez-KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb\_0)on QuipuSwap DEX |
| admin           | address                                                                                              | Administrator of the contract                                                                                                |
| pending\_admin  | address                                                                                              | Pending administrator that should accept his new administrator role (if it is possible)                                      |
| burner          | address                                                                                              | [Burner](../burner-contract/) contract address                                                                               |
| baker\_registry | address                                                                                              | [BakerRegistry](../bakerregistry-contract/) contract address                                                                 |
| farms\_count    | nat                                                                                                  | Number of farms created on this contract                                                                                     |

```pascaligo
type storage_type       is [@layout:comb] record [
  farms                   : big_map(fid_type, farm_type);
  referrers               : big_map(address, address);
  users_info              : big_map((fid_type * address), user_info_type);
  votes                   : big_map((fid_type * key_hash), nat);
  candidates              : big_map((fid_type * address), key_hash);
  banned_bakers           : big_map(key_hash, baker_type);
  token_metadata          : big_map(fid_type, tok_meta_type);
  qsgov                   : fa2_type;
  qsgov_lp                : address;
  admin                   : address;
  pending_admin           : address;
  burner                  : address;
  baker_registry          : address;
  farms_count             : nat;
]
```

### full\_storage\_type - storage root

| Field            | Type                                                         | Description                                                                                                           |
| ---------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| storage          | [storage\_type](storage-and-types-overview.md#storage\_type) | Actual storage of the contract                                                                                        |
| t\_farm\_lambdas | big\_map(nat, bytes)                                         | Contract's lambda-methods                                                                                             |
| metadata         | big\_map(string, bytes)                                      | Contract's metadata according to [TZIP-016](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-16/tzip-16.md) |

```pascaligo
type full_storage_type  is [@layout:comb] record [
  storage                 : storage_type;
  t_farm_lambdas          : big_map(nat, bytes);
  metadata                : big_map(string, bytes);
]
```
