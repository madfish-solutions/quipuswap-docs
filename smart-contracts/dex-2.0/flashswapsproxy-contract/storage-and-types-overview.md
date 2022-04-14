# Storage and types overview

### storage\_t - main contract storage

```pascaligo
type storage_t          is [@layout:comb] record [
  dex_core                : address;
]
```

| Field     | Type    | Description                   |
| --------- | ------- | ----------------------------- |
| dex\_core | address | Address of a DexCore contract |
