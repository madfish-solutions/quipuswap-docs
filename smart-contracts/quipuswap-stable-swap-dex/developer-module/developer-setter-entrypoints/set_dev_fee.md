# set\_dev\_fee

Sets developer fee rate. Input value is `nat`.

{% hint style="info" %}
Fee stored as float value multiplied by `fee_denominator` = $$10^{10}$$
{% endhint %}

### Parameters

| Field |  Type | Description                                                                                                                          |
| ----- | :---: | ------------------------------------------------------------------------------------------------------------------------------------ |
| -     | `nat` | Developer fee value. This value is a percent from value (where $$10^{10} = 100\%$$). Dev fee percent couldn't be more than $$50\%$$. |
