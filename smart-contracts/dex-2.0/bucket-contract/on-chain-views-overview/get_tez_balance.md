# get\_tez\_balance

This on-chain view returns TEZ tokens balance of the Bucket contract.

### Call parameters

A view doesn't accept any parameters.

### Return type

```pascaligo
nat
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const bucketAddress = "KT1...";
const viewCaller = "tz1...";
const bucket = await tezos.contract.at(bucketAddress);
const tezBalance = await bucket.contract.contractViews.get_tez_balance().executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

A view doesn't throw any errors.
