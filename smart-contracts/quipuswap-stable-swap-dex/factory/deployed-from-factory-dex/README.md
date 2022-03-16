# 💱 Deployed from factory DEX

This contract would be deployed after calling [add\_pool.md](../initialize-new-dex-flow/add\_pool.md "mention") the Factory entrypoint. Contract is almost close to Standalone version of DEX contract by ABI and storage. The distinction of contracts described in [#the-main-difference-in-implementations](../../#the-main-difference-in-implementations "mention").

### Initialization of contract

The initialization section describes methods that are called **only** by the `Factory` contract. These methods are included in [start\_dex.md](../initialize-new-dex-flow/start\_dex.md "mention") call and used for initial setup and start DEX pool.

{% content-ref url="initialization/" %}
[initialization](initialization/)
{% endcontent-ref %}

### Contract storage

Storage of contract differs from Standalone only with excluding developer config in exchange of adding factory address and pausing of contract.

{% content-ref url="storage-and-types-overview.md" %}
[storage-and-types-overview.md](storage-and-types-overview.md)
{% endcontent-ref %}

### Core DEX methods

Main methods of DEX, that are able to use by anyone. These methods include investing, swapping, and divesting. Also, there are additional methods for staking QUIPU tokens for earning additional rewards and claiming referral rewards.

{% content-ref url="../../standalone-dex/dex-methods/" %}
[dex-methods](../../standalone-dex/dex-methods/)
{% endcontent-ref %}

### Developer method

{% hint style="warning" %}
This entrypoint should be called only by `developer` address of Factory contract.&#x20;
{% endhint %}

This entrypoint is designed to claim developer rewards from a specific contract (DEX pool).

{% content-ref url="../../standalone-dex/developer-methods/claim_developer.md" %}
[claim\_developer.md](../../standalone-dex/developer-methods/claim\_developer.md)
{% endcontent-ref %}

### Admin methods

{% hint style="warning" %}
These entrypoints should be called only by `admin` address.&#x20;
{% endhint %}

The next section is about entrypoints for managing fees, "A" constant change, editing the manager list, and changing an admin address.

{% content-ref url="../../standalone-dex/admin-methods/" %}
[admin-methods](../../standalone-dex/admin-methods/)
{% endcontent-ref %}
