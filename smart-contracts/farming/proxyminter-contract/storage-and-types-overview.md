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

| Field          | Type                                                 | Description                                                                             |
| -------------- | ---------------------------------------------------- | --------------------------------------------------------------------------------------- |
| minters        | set(address)                                         | Set of registered by admin minters                                                      |
| qsgov          | [fa2\_type](storage-and-types-overview.md#fa2\_type) | QuipuSwap Governance token info (address and token ID)                                  |
| admin          | address                                              | Administrator of the contract                                                           |
| pending\_admin | address                                              | Pending administrator that should accept his new administrator role (if it is possible) |

```pascaligo
type storage_type       is [@layout:comb] record [
  minters                 : set(address);
  qsgov                   : fa2_type;
  admin                   : address;
  pending_admin           : address;
]
```
