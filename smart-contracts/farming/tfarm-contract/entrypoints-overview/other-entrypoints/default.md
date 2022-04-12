# default

An entrypoint that receives TEZ which were mistakenly sent to the contract and transfers them to the [Burner](../../../burner-contract/) contract.

### Call parameters

An entrypoint doesn't accept any parameters.

{% hint style="danger" %}
Note: you need to pass positive TEZ/mutez amount to _**send()**_** ** method (see example below).
{% endhint %}

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const mutezAmount = 100;
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.default([]).send({ amount: mutezAmount, mutez: true });

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

An entrypoint doesn't throw any error.
