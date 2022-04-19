# pour\_out

An entrypoint that withdraws TEZ tokens to the receiver from the parameters (mostly to the [DexCore](../../dexcore-contract/) contract).

### Call parameters

```pascaligo
type pour_out_t         is [@layout:comb] record [
  receiver                : contract(unit);
  amt                     : nat;
]
```

| Field    | Type           | Description            |
| -------- | -------------- | ---------------------- |
| receiver | contract(unit) | Receiver of TEZ tokens |
| amt      | nat            | Amount to withdraw     |

### Usage

Only [DexCore](../../dexcore-contract/) contract can call this entrypoint.

### Errors

* `403` - `sender` of the transaction is not [DexCore](../../dexcore-contract/) contract.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
