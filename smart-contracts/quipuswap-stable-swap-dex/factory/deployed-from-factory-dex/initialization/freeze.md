# freeze

{% hint style="warning" %}
This entrypoint should be called only by `Factory` contract address.&#x20;
{% endhint %}

{% hint style="info" %}
The DEX pool contract deploys with `started = False`. This method changes this field.
{% endhint %}

This method is used only to trigger "unfreeze" of the contract after copying DEX lambdas - the last needed lambdas to enable full functionality of DEX pool.

Receives `unit` type.

Inverts value of the `started` field of contract. Called only once after setting all lambdas to DEX pool contract.
