# 🛑 Developer methods

{% hint style="warning" %}
These sections are called only by `developer` address.
{% endhint %}

### Claim collected deployment fees.

The Factory contract charges a deployment fee in [QUIPU](https://better-call.dev/mainnet/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/metadata) token. Some of the tokens got burnt and some goes to reserves. The `developer` could withdraw this fee reward.

{% hint style="info" %}
This method withdraws all the reserves in one call.&#x20;
{% endhint %}

{% content-ref url="claim_rewards.md" %}
[claim\_rewards.md](claim\_rewards.md)
{% endcontent-ref %}

### Factory management

The `developer` as admin of contract performs management of the contract. Management includes deployment fee price, burn percent, and the whitelisted addresses. Also, all params of [developer-module](../../developer-module/ "mention") presents inside the management section.

{% content-ref url="factory-management/" %}
[factory-management](factory-management/)
{% endcontent-ref %}
