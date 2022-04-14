# default

An entrypoint that receives bakers' rewards and updates global rewards for all users.

### Call parameters

An entrypoint doesn't accept any parameters.

{% hint style="danger" %}
Note: you need to pass positive TEZ/mutez amount to the _**send()**_** ** method (see example below).
{% endhint %}

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const bucketAddress = "KT1...";
const mutezAmount = 100;
const bucket = await tezos.contract.at(bucketAddress);
const operation = await bucket.methods.default([]).send({ amount: mutezAmount, mutez: true });

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

An entrypoint doesn't throw any errors.
