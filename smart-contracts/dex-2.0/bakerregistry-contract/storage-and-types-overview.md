# Storage and types overview

### storage\_t - main contract storage

```pascaligo
type storage_t          is big_map(key_hash, bool)
```

| Field      | Type                      | Description                                                                                                               |
| ---------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| storage\_t | big\_map(key\_hash, bool) | Mapping of bakers' addresses to boolean flag: baker is registered in registry or not. Only valid bakers can be registered |
