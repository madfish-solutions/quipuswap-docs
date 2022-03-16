# DEX compiled codebase setup

{% hint style="warning" %}
This contract method are called only by `developer` of Factory.
{% endhint %}

### Admin lambdas

This entrypoint sets [admin-methods](../../../standalone-dex/admin-methods/ "mention") lambda-functions to contract storage by function ID and function-packed bytes. &#x20;

{% content-ref url="../../../standalone-dex/initialization/set_admin_function.md" %}
[set\_admin\_function.md](../../../standalone-dex/initialization/set\_admin\_function.md)
{% endcontent-ref %}

### DEX lambdas

This entrypoint sets [dex-methods](../../../standalone-dex/dex-methods/ "mention") lambda-functions to contract storage by function ID and function-packed bytes. &#x20;

{% content-ref url="../../../standalone-dex/initialization/set_dex_function.md" %}
[set\_dex\_function.md](../../../standalone-dex/initialization/set\_dex\_function.md)
{% endcontent-ref %}

### FA2 standard lambdas

This entrypoint sets FA2 interface lambda-functions to contract storage by function ID and function-packed bytes. &#x20;

{% content-ref url="../../../standalone-dex/initialization/set_token_function.md" %}
[set\_token\_function.md](../../../standalone-dex/initialization/set\_token\_function.md)
{% endcontent-ref %}
