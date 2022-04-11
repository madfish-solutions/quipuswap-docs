# Storage and types overview

### fa2\_type

| Field | Type                  | Description        |
| ----- | --------------------- | ------------------ |
| token | address               | Token's address    |
| id    | token\_id\_type (nat) | Token's identifier |

```pascaligo
type fa2_type           is [@layout:comb] record [
  token                   : address;
  id                      : token_id_type;
]
```

### storage\_type - main contract storage

| Field     | Type                                                 | Description                                                                                                                  |
| --------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| qsgov\_lp | address                                              | Address of the [QUIPU/TEZ LP token ](https://quipuswap.com/swap/tez-KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb\_0)on QuipuSwap DEX |
| qsgov     | [fa2\_type](storage-and-types-overview.md#fa2\_type) | QuipuSwap Governance token info (address and token ID)                                                                       |

```pascaligo
type storage_type       is [@layout:comb] record [
  qsgov_lp                : address;
  qsgov                   : fa2_type;
]
```
