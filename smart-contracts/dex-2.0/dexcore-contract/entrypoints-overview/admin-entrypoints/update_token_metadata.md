# update\_token\_metadata

An entrypoint that updates LP token metadata. Also can add a new fields to an existing metadata.

### Call parameters

```pascaligo
type metadata_pair_t    is [@layout:comb] record [
  key                     : string;
  value                   : bytes;
]

type upd_tok_meta_t     is [@layout:comb] record [
  token_id                : token_id_t;
  token_info              : list(metadata_pair_t);
]
```

#### metadata\_pair\_t

| Field | Type   | Description    |
| ----- | ------ | -------------- |
| key   | string | Metadata key   |
| value | bytes  | Metadata value |

#### upd\_tok\_meta\_t

| Field       | Type                                                                    | Description         |
| ----------- | ----------------------------------------------------------------------- | ------------------- |
| token\_id   | token\_id\_t (nat)                                                      | Token's (pool's) ID |
| token\_info | list([metadata\_pair\_t](update\_token\_metadata.md#metadata\_pair\_t)) | Token's metadata    |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = {
    token_id: 1,
    token_info: [
        {
           key: "name",
           value: Buffer.from("wWBTC/TEZ LP").toString("hex"),
        },
        {
           key: "new_field",
           value: Buffer.from("New value").toString("hex"),
        },
        ...
    ],
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.update_token_metadata(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `402` - `sender` of the transaction is not a manager.
