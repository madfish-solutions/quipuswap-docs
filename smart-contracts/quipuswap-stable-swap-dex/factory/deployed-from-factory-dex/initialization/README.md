# 🟡 Initialization

There are two entrypoints are responsible for initializing the new DEX pool contract.

{% hint style="warning" %}
These entrypoints should be called only by `Factory` contract address.&#x20;
{% endhint %}

Both methods are called as internal operations of one entrypoint of Factory: [start\_dex.md](../../initialize-new-dex-flow/start\_dex.md "mention").

### Copy core dex lambdas

This method receives big\_map of `nat -> bytes` - lambdas of [dex-methods](../../../standalone-dex/dex-methods/ "mention").

{% content-ref url="copy_dex_function.md" %}
[copy\_dex\_function.md](copy\_dex\_function.md)
{% endcontent-ref %}

### Freeze

{% hint style="info" %}
The DEX pool contract deploys with `started = False`. This method changes this field.
{% endhint %}

This method is used only to trigger "unfreeze" of the contract after copying DEX lambdas - the last needed lambdas to enable full functionality of DEX pool.

{% content-ref url="freeze.md" %}
[freeze.md](freeze.md)
{% endcontent-ref %}
