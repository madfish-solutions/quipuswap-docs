# set\_baker\_registry

An entrypoint that setups a new **BakerRegistry** contract for bakers validation and registration in time of voting (see [BakerRegistry](../../../bakerregistry-contract/)).

### Call parameters

| Field           | Type    | Description                                    |
| --------------- | ------- | ---------------------------------------------- |
| baker\_registry | address | An address of a new **BakerRegistry** contract |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const bakerRegistry = "KT1...";
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.set_baker_registry(bakerRegistry).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
