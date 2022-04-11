# update\_token\_metadata

An entrypoint that updates share token metadata. Also can add new fields.

### Call parameters

```pascaligo
type meta_pair_type     is [@layout:comb] record [
  key                     : string;
  value                   : bytes;
]

type upd_tok_meta_type  is [@layout:comb] record [
  token_id                : nat;
  token_info              : list(meta_pair_type);
]
```

#### meta\_pair\_type

| Field | Type   | Description    |
| ----- | ------ | -------------- |
| key   | string | Metadata key   |
| value | bytes  | Metadata value |

#### upd\_tok\_meta\_type

| Field       | Type                                                                  | Description         |
| ----------- | --------------------------------------------------------------------- | ------------------- |
| token\_id   | nat                                                                   | Token's (farm's) ID |
| token\_info | list([meta\_pair\_type](update\_token\_metadata.md#meta\_pair\_type)) | Token's metadata    |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const tFarmAddress = "KT1...";
const params = {
    token_id: 1,
    token_info: [
        {
           key: "name",
           value: Buffer.from("wWBTC/TEZ FA2 Staking Share").toString("hex"),
        },
        {
           key: "new_field",
           value: Buffer.from("New value").toString("hex"),
        },
        ...
    ],
};
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methodsObject.update_token_metadata(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
