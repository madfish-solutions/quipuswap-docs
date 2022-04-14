# Storage and types overview

### user\_reward\_info\_t

| Field           | Type | Hint                            | Description                           |
| --------------- | ---- | ------------------------------- | ------------------------------------- |
| reward\_f       | nat  | Float value multiplied by 1e+18 | Reward that must be paid to a user    |
| reward\_paid\_f | nat  | Float value multiplied by 1e+18 | Reward that is already paid to a user |

```pascaligo
type user_reward_info_t is [@layout:comb] record [
  reward_f                : nat;
  reward_paid_f           : nat;
]
```

### baker\_t

| Field            | Type      | Description                                     |
| ---------------- | --------- | ----------------------------------------------- |
| ban\_start\_time | timestamp | Start timestamp of baker's banning period       |
| ban\_period      | nat       | Banning period duration (in seconds)            |
| votes            | nat       | Amount of votes delegated to baker by all users |

```pascaligo
type baker_t            is [@layout:comb] record [
  ban_start_time          : timestamp;
  ban_period              : nat;
  votes                   : nat;
]
```

### user\_t

| Field     | Type              | Description                                       |
| --------- | ----------------- | ------------------------------------------------- |
| candidate | option(key\_hash) | Baker candidate of a user                         |
| votes     | nat               | Amount of votes delegated to the user's candidate |

```pascaligo
type user_t             is [@layout:comb] record [
  candidate               : option(key_hash);
  votes                   : nat;
]
```

### storage\_t - main contract storage

| Field                   | Type                                                                                | Description                                                                                 |
| ----------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| users                   | big\_map(address, [user\_t](storage-and-types-overview.md#user\_t))                 | Mapping of users' addresses to theirs info                                                  |
| bakers                  | big\_map(key\_hash, [baker\_t](storage-and-types-overview.md#baker\_t))             | Mapping of bakers' addresses to theirs info                                                 |
| users\_rewards          | big\_map(address, [user\_reward\_info\_t](storage-and-types-overview.md#undefined)) | Mapping of users' addresses to theirs reward info                                           |
| previous\_delegated     | key\_hash                                                                           | Previous delegate                                                                           |
| current\_delegated      | key\_hash                                                                           | Current delegate                                                                            |
| next\_candidate         | key\_hash                                                                           | Next possible delegate                                                                      |
| baker\_registry         | address                                                                             | [BakerRegistry](../bakerregistry-contract/) contract address                                |
| dex\_core               | address                                                                             | [DexCore](../dexcore-contract/) contract address                                            |
| pair\_id                | token\_id\_t                                                                        | Pair ID on [DexCore](../dexcore-contract/) contract to which the current contract is linked |
| next\_reward            | nat                                                                                 | Accumulator for bakers' rewards that will be distributed between all voters                 |
| total\_reward           | nat                                                                                 | Total rewards that will be distributed among all voters                                     |
| reward\_paid            | nat                                                                                 | Amount of paid to users bakers' rewards                                                     |
| reward\_per\_share      | nat                                                                                 | Accumulator for reward per 1 staked token's unit                                            |
| reward\_per\_block      | nat                                                                                 | Reward per 1 block                                                                          |
| last\_update\_level     | nat                                                                                 | Level when a rewards were updated last time                                                 |
| collecting\_period\_end | nat                                                                                 | Level when rewards will be collected and distributed among all voters                       |

```pascaligo
type storage_t          is [@layout:comb] record [
  users                   : big_map(address, user_t);
  bakers                  : big_map(key_hash, baker_t);
  users_rewards           : big_map(address, user_reward_info_t);
  previous_delegated      : key_hash;
  current_delegated       : key_hash;
  next_candidate          : key_hash;
  baker_registry          : address;
  dex_core                : address;
  pair_id                 : token_id_t;
  next_reward             : nat;
  total_reward            : nat;
  reward_paid             : nat;
  reward_per_share        : nat;
  reward_per_block        : nat;
  last_update_level       : nat;
  collecting_period_end   : nat;
]
```
