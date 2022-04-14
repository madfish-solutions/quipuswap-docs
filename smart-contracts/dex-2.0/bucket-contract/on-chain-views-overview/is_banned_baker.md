# is\_banned\_baker

This on-chain view checks baker is banned on this Bucket contract or not.

### Call parameters

| Field | Type      | Description    |
| ----- | --------- | -------------- |
| baker | key\_hash | Baker to check |

### Return type

```pascaligo
nat
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const bucketAddress = "KT1...";
const baker = "tz1...";
const viewCaller = "tz1...";
const bucket = await tezos.contract.at(bucketAddress);
const isBannedBaker = await bucket.contract.contractViews.is_banned_baker(baker).executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

A view doesn't throw any errors.
