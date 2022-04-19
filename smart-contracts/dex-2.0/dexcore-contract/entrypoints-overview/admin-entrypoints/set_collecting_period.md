# set\_collecting\_period

An entrypoint that setups a collection period (in blocks) during which bakers' rewards will be collected before distribution.

### Call parameters

| Field              | Type | Description                               |
| ------------------ | ---- | ----------------------------------------- |
| collecting\_period | nat  | Duration of a collecting period in blocks |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const collectingPeriod = 2048;
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methods.set_collecting_period(collectingPeriod).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
