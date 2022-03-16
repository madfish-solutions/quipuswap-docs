# set\_fees

{% hint style="warning" %}
This entrypoint should be called only by `admin` address.
{% endhint %}

This entrypoint is designed to update fee rates.

More info about fee storage and precisions, please, read [#fee-storage-fee-rates-record](../storage-and-types-overview.md#fee-storage-fee-rates-record "mention") section.

### Call params

```pascaligo
type fees_storage_t     is [@layout:comb] record [
  lp                      : nat; 
  stakers                 : nat;
  ref                     : nat;
]

type set_fee_param_t    is [@layout:comb] record [
  pool_id                 : pool_id_t;
  fee                     : fees_storage_t;
]
```
