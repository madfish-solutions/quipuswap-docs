# get\_collecting\_period

This on-chain view returns collecting period (in blocks) that is used for bakers' rewards collecting.

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
const dexCoreAddress = "KT1...";
const viewCaller = "tz1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const collectingPeriod = await dexCore.contract.contractViews.get_collecting_period().executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

A view doesn't throw any errors.
