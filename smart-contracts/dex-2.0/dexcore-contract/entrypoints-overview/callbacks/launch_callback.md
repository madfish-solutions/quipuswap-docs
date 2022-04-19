# launch\_callback

An additional entrypoint that helps to [vote](../../../bucket-contract/entrypoints-overview/vote.md) in [Bucket](../../../bucket-contract/) contract for a user's baker in time of the first TOK/TEZ exchange launch.

### Call parameters

```pascaligo
type vote_t             is [@layout:comb] record [
  voter                   : address;
  candidate               : key_hash;
  execute_voting          : bool;
  votes                   : nat;
  current_balance         : nat;
]

type launch_callback_t  is [@layout:comb] record [
  vote_params             : vote_t;
  bucket                  : address;
]
```

#### vote\_t

| Field            | Type      | Description                                  |
| ---------------- | --------- | -------------------------------------------- |
| voter            | address   | A user who votes                             |
| candidate        | key\_hash | Baker the user votes for                     |
| execute\_voting  | bool      | Flag that indicates: execute voting or not   |
| votes            | nat       | Amount of votes that will be used for voting |
| current\_balance | nat       | User's current LP tokens balance             |

#### launch\_callback\_t

| Field        | Type                                   | Description                                                                       |
| ------------ | -------------------------------------- | --------------------------------------------------------------------------------- |
| vote\_params | [vote\_t](launch\_callback.md#vote\_t) | Voting parameters                                                                 |
| bucket       | address                                | [Bucket](../../../bucket-contract/) contract address where need to execute voting |

### Usage

Only [DexCore](../../) contract can call this entrypoint.

### Errors

* `138` - only entered (transaction must be not the first transaction in the chain of calls).
* `403` - `sender` of the transaction is not [DexCore](../../) contract.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
