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

### Storage - main contract storage

| Field             |            Type           | Hint                                                                                                                                                                                                           | Description                                                                                                                                 |
| ----------------- | :-----------------------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| dev\_store        |      `dev_storage_t`      |                                                                                                                                                                                                                | [#developer-storage](../developer-module/storage-and-action-types.md#developer-storage "mention")                                           |
| init\_price       |           `nat`           |                                                                                                                                                                                                                | Amount of QUIPU tokens to be charged when deploy of DEX called.                                                                             |
| burn\_rate        |           `nat`           | float value. multiplied by $$10^6$$                                                                                                                                                                            | Persent of QUIPU charges to be sent to zero address.                                                                                        |
| pools\_count      |           `nat`           | Counter                                                                                                                                                                                                        | Amount of pools created by current contract.                                                                                                |
| pool\_to\_address | `big_map(bytes, address)` | Bytes - packed by `Bytes.pack(key)` where key is `record[ tokens=tokens; deployer=deployer]`  where tokens is valid `tokens_map_t` (sorted tokens) and deployer is address of user that deployed DEX contract. | Mapping that allows finding pool address by packed bytes of record with fields `tokens` of `tokens_map_t` type and `deployer` of `address`. |
| quipu\_token      |       `fa2_token_t`       |                                                                                                                                                                                                                | QUIPU token address and token ID                                                                                                            |
| quipu\_rewards    |           `nat`           |                                                                                                                                                                                                                | Collected QUIPU tokens from deploy (without sent to zero address).                                                                          |
| whitelist         |       `set(address)`      |                                                                                                                                                                                                                | set of addresses that allowed to deploy without QUIPU charges.                                                                              |

```pascaligo
type inner_store_t      is [@layout:comb] record[
  dev_store               : dev_storage_t;
  init_price              : nat; (* Pool creation price in QUIPU token *)
  burn_rate               : nat; (* Percent of QUIPU tokens to be burned *)
  pools_count             : nat;
  pool_to_address         : big_map(bytes, address);
  quipu_token             : fa2_token_t;
  quipu_rewards           : nat;
  whitelist               : set(address);
]
```

### Full storage type - storage root

| Field          |          Type         | Hint                                                                                                    | Description                                       |
| -------------- | :-------------------: | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| storage        |    `inner_store_t`    | [#storage-main-contract-storage](storage-and-types-overview.md#storage-main-contract-storage "mention") | Main configuration and contract values of factory |
| admin\_lambdas | `big_map(nat, bytes)` |                                                                                                         | Administrative lambda-methods storage             |
| dex\_lambdas   | `big_map(nat, bytes)` |                                                                                                         | DEX stable swap protocol lambda-methods storage   |
| token\_lambdas | `big_map(nat, bytes)` |                                                                                                         | FA2 lambda-methods storage                        |
| init\_func     |    `option(bytes)`    |                                                                                                         | lambda function for deploying new DEX             |

```pascaligo
type full_storage_t     is [@layout:comb] record [
  storage                 : inner_store_t;
  admin_lambdas           : big_map(nat, bytes); (* map with admin-related functions code *)
  dex_lambdas             : big_map(nat, bytes); (* map with exchange-related functions code *)
  token_lambdas           : big_map(nat, bytes); (* map with token-related functions code *)
  init_func               : option(bytes); (* lambda function for deploying new DEX *)
]
```
