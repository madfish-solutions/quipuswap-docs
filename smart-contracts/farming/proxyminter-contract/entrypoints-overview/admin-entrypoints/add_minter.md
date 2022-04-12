# add\_minter

An entrypoint that adds or removes minters that can interact with [mint\_tokens](../minter-entrypoint/mint\_tokens.md) entrypoint.

### Call parameters

```pascaligo
type add_minter_type    is [@layout:comb] record [
  minter                  : address;
  register                : bool;
]
```

| Field    | Type    | Description                                         |
| -------- | ------- | --------------------------------------------------- |
| minter   | address | An address of a minter to add or remove             |
| register | bool    | Flag that indicates: admin adds a minter or removes |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const proxyMinterAddress = "KT1...";
const params = {
    minter: "tz1.../KT1...",
    add: true, // false - to remove a minter
};
const proxyMinter = await tezos.contract.at(proxyMinterAddress);
const operation = await proxyMinter.methodsObject.add_minter(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
