# vote

An entrypoint that executes voting for a bakers on this Bucket contract. Also it updates users' global rewards and the rewards of the user who votes.

### Call parameters

```pascaligo
type vote_t             is [@layout:comb] record [
  voter                   : address;
  candidate               : key_hash;
  execute_voting          : bool;
  votes                   : nat;
]
```

| Field           | Type      | Description                                  |
| --------------- | --------- | -------------------------------------------- |
| voter           | address   | A user who votes                             |
| candidate       | key\_hash | Baker the user votes for                     |
| execute\_voting | bool      | Flag that indicates: execute voting or not   |
| votes           | nat       | Amount of votes that will be used for voting |

### Usage

Only [DexCore](../../dexcore-contract/) contract can call this entrypoint.

### Errors

* `403` - `sender` of the transaction is not [DexCore](../../dexcore-contract/) contract.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
