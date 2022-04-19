# close

An additional entrypoint that helps to prevent reentrancy attacks. It changes the state checker and finishes the chain of transaction calls.

### Call parameters

```pascaligo
type close_t            is unit
```

### Usage

Only [DexCore](../../) contract can call this entrypoint.

### Errors

* `138` - only entered (transaction must be not the first transaction in the chain of calls).
* `403` - `sender` of the transaction is not [DexCore](../../) contract.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
