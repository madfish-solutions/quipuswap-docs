# confirm\_admin

An entrypoint for a pending administrator. A pending administrator must just call it and he will become a new administrator of the contract.

### Call parameters

An entrypoint doesn't accept any parameters.

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.confirm_admin([]).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-pending-admin` - `sender` of the transaction is not current pending administrator (not the address that was assigned by the current administrator to the shift).
