# copy\_dex\_function

{% hint style="warning" %}
This entrypoint should be called only by `Factory` contract address.&#x20;
{% endhint %}

This method receives `big_map` of `nat -> bytes` - lambdas of [dex-methods](../../../standalone-dex/dex-methods/ "mention").

### Parameters

| Field |          Type         | Description                                     |
| ----- | :-------------------: | ----------------------------------------------- |
| -     | `big_map(nat, bytes)` | mapping of index and bytes of DEX core methods. |
