# ban\_baker

An entrypoint that bans or unbans bakers on this Bucket contract. Voting for a banned baker is not possible.

### Call parameters

```pascaligo
type ban_baker_t        is [@layout:comb] record [
  baker                   : key_hash;
  ban_period              : nat;
]
```

| Field       | Type      | Description                         |
| ----------- | --------- | ----------------------------------- |
| baker       | key\_hash | Baker for banning or unbanning      |
| ban\_period | nat       | Period for ban (0 to unban a baker) |

### Usage

Only [DexCore](../../dexcore-contract/) contract can call this entrypoint.

### Errors

* `403` - `sender` of the transaction is not [DexCore](../../dexcore-contract/) contract.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
