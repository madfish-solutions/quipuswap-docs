# 🟡 Initial setup

{% hint style="warning" %}
This section called only by `developer` address.
{% endhint %}

### DEX deploy function lambda

{% content-ref url="set_init_function.md" %}
[set\_init\_function.md](set\_init\_function.md)
{% endcontent-ref %}

### Developer lambdas

This entrypoint sets [developer-setter-entrypoints](../../developer-module/developer-setter-entrypoints/ "mention") lambda-functions to contract storage by function ID and function-packed bytes. &#x20;

{% content-ref url="../../standalone-dex/initialization/set_dev_function.md" %}
[set\_dev\_function.md](../../standalone-dex/initialization/set\_dev\_function.md)
{% endcontent-ref %}

### Pre-compiled DEX lambdas

These entrypoints are designed for setting lambdas that will be copied and used in deployed DEX pool contracts.

{% content-ref url="dex-compiled-codebase-setup/" %}
[dex-compiled-codebase-setup](dex-compiled-codebase-setup/)
{% endcontent-ref %}
