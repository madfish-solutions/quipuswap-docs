# validate

An entrypoint for bakers validation. If baker is not registered and valid, he will be registered.

### Call parameters

| Field | Type      | Description           |
| ----- | --------- | --------------------- |
| baker | key\_hash | An address of a baker |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```java
const bakerRegistryAddress = "KT1...";
const baker = "tz1...";
const bakerRegistry = await tezos.contract.at(bakerRegistryAddress);
const operation = await bakerRegistry.methods.validate(baker).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

Operation fails in time of baker registration when the key\_hash parameter is not a registered delegate (standard Tezos error).
