# pour\_over

An entrypoint that sends TEZ tokens to another Bucket contract. This is necessary during the [_**swap**_](../../dexcore-contract/entrypoints-overview/dex-entrypoints/swap.md) operation in order to immediately transfer TEZ tokens from one Bucket contract to another and not make unnecessary [_**pour\_out**_](pour\_out.md) and [_**fill**_](fill.md) operations.

### Call parameters

```pascaligo
type pour_over_t        is [@layout:comb] record [
  bucket                  : address;
  amt                     : nat;
]
```

| Field  | Type    | Description                                         |
| ------ | ------- | --------------------------------------------------- |
| bucket | address | Bucket contract address for receiving of TEZ tokens |
| amt    | nat     | Amount to send                                      |

### Usage

Only [DexCore](../../dexcore-contract/) contract can call this entrypoint.

### Errors

* `403` - `sender` of the transaction is not [DexCore](../../dexcore-contract/) contract.
