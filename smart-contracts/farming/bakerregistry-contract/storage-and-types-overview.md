# Storage and types overview

### storage\_type - main contract storage

Mapping of bakers' addresses to boolean flag: baker is registered in registry or not. Only valid bakers can be registered.

```pascal
type storage_type       is big_map(key_hash, bool)
```
