# receive\_fee

An entrypoint that receives auction fee from the [DexCore](../../../dexcore-contract/) contract (see [_**withdraw\_auction\_fee**_](../../../dexcore-contract/entrypoints-overview/dex-entrypoints/withdraw\_auction\_fee.md) entrypoint), calculates dev and public fees and stores these values in the contract's storage.

### Call parameters

```pascaligo
type tez_t              is unit

type fa12_token_t       is address

type fa2_token_t        is [@layout:comb] record [
  token                   : address;
  id                      : nat;
]

type token_t            is
| Tez                     of tez_t
| Fa12                    of fa12_token_t
| Fa2                     of fa2_token_t

type receive_fee_t      is [@layout:comb] record [
  token                   : token_t;
  fee                     : nat;
]
```

| Field | Type     | Description         |
| ----- | -------- | ------------------- |
| token | token\_t | FA1.2/FA2/TEZ token |
| fee   | nat      | Received fee amount |

### Usage

Only [DexCore](../../../dexcore-contract/) contract can call this entrypoint.

### Errors

* `403` - `sender` of the transaction is not [DexCore](../../../dexcore-contract/) contract.
