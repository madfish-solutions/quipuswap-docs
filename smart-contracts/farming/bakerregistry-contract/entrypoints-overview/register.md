# register

An entrypoint for bakers registration.

### Call parameters

| Field | Type      | Description           |
| ----- | --------- | --------------------- |
| baker | key\_hash | An address of a baker |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const bakerRegistryAddress = "KT1...";
const baker = "tz1...";
const bakerRegistry = await tezos.contract.at(bakerRegistryAddress);
const operation = await bakerRegistry.methods.register(baker).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

Operation fails when the key\_hash parameter is not a registered delegate (standard Tezos error).
