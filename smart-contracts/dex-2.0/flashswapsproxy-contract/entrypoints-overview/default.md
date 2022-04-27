# default

An entrypoint that accepts users' lambdas during a [_**flash\_swap**_](../../dexcore-contract/entrypoints-overview/dex-entrypoints/swap.md) operations on [_**DexCore**_](../../dexcore-contract/) contract and executes them.

### Call parameters

```pascaligo
type default_t          is unit -> list(operation)
```

| Field      | Type                    | Description                                                                                                                     |
| ---------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| default\_t | unit -> list(operation) | Users's lambda function that doesn't accept any parameters (_**unit**_) and returns a list of operations (transactions, calls). |

### Usage

Only [_**DexCore**_](../../dexcore-contract/) contract can call this entrypoint.

### Errors

* `403` - `sender` of the transaction is not [DexCore](../../dexcore-contract/) contract.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
