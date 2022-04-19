# add\_managers

An entrypoint that adds or removes a managers who can update LP tokens metadata.

### Call parameters

```pascaligo
type add_manager_t      is [@layout:comb] record [
  manager                 : address;
  add                     : bool;
]

type add_managers_t     is list(add_manager_t)
```

| Field   | Type    | Description                                  |
| ------- | ------- | -------------------------------------------- |
| manager | address | Account of a manager                         |
| add     | bool    | Flag that indicates: add or remove a manager |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const params = [
    {
        manager: "tz1.../KT1...",
        add: true, // or false
    },
    ...
];
const operation = await dexCore.methods.add_managers(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
