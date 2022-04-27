# withdraw\_rewards

An entrypoint that updates users' global rewards. Also it updates the rewards of the user who wants to make a withdrawal. After all updates it executes a withdrawal of bakers' rewards for the specified user.

### Call parameters

```pascaligo
type withdraw_rewards_t is [@layout:comb] record [
  receiver                : contract(unit);
  user                    : address;
]
```

| Field    | Type           | Description                             |
| -------- | -------------- | --------------------------------------- |
| receiver | contract(unit) | Receiver of TEZ tokens                  |
| user     | address        | User whose rewards need to be withdrawn |

### Usage

Only [DexCore](../../dexcore-contract/) contract can call this entrypoint.

### Errors

* `403` - `sender` of the transaction is not [DexCore](../../dexcore-contract/) contract.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
