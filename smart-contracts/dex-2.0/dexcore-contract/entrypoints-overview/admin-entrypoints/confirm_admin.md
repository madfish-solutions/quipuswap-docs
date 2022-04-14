# confirm\_admin

An entrypoint for a pending administrator. A pending administrator must just call it and he will become a new administrator of the contract.

### Call parameters

An entrypoint doesn't accept any parameters.

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methods.confirm_admin([]).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `401` - `sender` of the transaction is not current pending administrator (not the address that was assigned by the current administrator to the shift).
* `411` - `pending_admin` in the storage is `None` (admin didn't call [_**set\_admin**_](set\_admin.md) entrypoint).
