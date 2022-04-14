# fill

An entrypoint that accepts TEZ tokens (mostly from [DexCore](../../dexcore-contract/) contract or other Bucket contracts), stores them on the contract and doesn't affect the distribution of baker rewards.

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
const operation = await bucket.methods.fill([]).send({ amount: mutezAmount, mutez: true });

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

An entrypoint doesn't throw any errors.
