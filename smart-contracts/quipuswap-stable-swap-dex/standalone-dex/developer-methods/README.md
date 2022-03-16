---
description: Manage developer fee, address and claim developer rewards
---

# 🛠 Developer methods

{% hint style="warning" %}
These entrypoints should be called only by `developer` address.&#x20;
{% endhint %}

### Manage developer info

Managing of developer info preforms by [developer-module](../../developer-module/ "mention"). More info about usage of setting developer config params is provided on the page below.

{% content-ref url="../../developer-module/developer-setter-entrypoints/" %}
[developer-setter-entrypoints](../../developer-module/developer-setter-entrypoints/)
{% endcontent-ref %}

### Claim rewards

Develper can claim part (or all) collected rewards by providing FA12/FA2 token and amount, that needed to receive. For this action is used entrypoint `claim_developer`.&#x20;

{% content-ref url="claim_developer.md" %}
[claim\_developer.md](claim\_developer.md)
{% endcontent-ref %}
