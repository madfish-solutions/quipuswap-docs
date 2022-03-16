# 🟡 Initialization

The initialization section includes documentation about entrypoints, that should be executed right **after deploy** and **before usage** of this contract.&#x20;

{% hint style="warning" %}
These contract methods are called only by `admin` of that contract.
{% endhint %}

### Admin lambdas

This entrypoint sets [admin-methods](../admin-methods/ "mention") lambda-functions to contract storage by function ID and function-packed bytes. &#x20;

{% content-ref url="set_admin_function.md" %}
[set\_admin\_function.md](set\_admin\_function.md)
{% endcontent-ref %}

### Developer lambdas

This entrypoint sets [developer-setter-entrypoints](../../developer-module/developer-setter-entrypoints/ "mention") lambda-functions to contract storage by function ID and function-packed bytes. &#x20;

{% content-ref url="set_dev_function.md" %}
[set\_dev\_function.md](set\_dev\_function.md)
{% endcontent-ref %}

### DEX lambdas

This entrypoint sets [dex-methods](../dex-methods/ "mention") lambda-functions to contract storage by function ID and function-packed bytes. &#x20;

{% content-ref url="set_dex_function.md" %}
[set\_dex\_function.md](set\_dex\_function.md)
{% endcontent-ref %}

### FA2 standard lambdas

This entrypoint sets FA2 interface lambda-functions to contract storage by function ID and function-packed bytes. &#x20;

{% content-ref url="set_token_function.md" %}
[set\_token\_function.md](set\_token\_function.md)
{% endcontent-ref %}
