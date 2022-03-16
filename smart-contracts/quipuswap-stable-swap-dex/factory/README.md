# 🏭 Factory

Factory is the implementation of DEX-as-a-service way to use DEX pool. Factory is used for deploying new DEX pools as separate contracts for some fee in QUIPU tokens. Also factory contract store and manage developer config from [developer-module](../developer-module/ "mention"). Also `developer` represents **admin** of factory contract.

### Storage

Factory storage contains init lambda, DEX contract lambdas, configuration of deploy price and burn rate, whitelist, and mapping of deployed pools.

{% content-ref url="storage-and-types-overview.md" %}
[storage-and-types-overview.md](storage-and-types-overview.md)
{% endcontent-ref %}

### Initialization of factory

Factory should store many methods, so some of that stored in lambdas inside storage. These lambdas should be set **before** usage of the contract.&#x20;

{% hint style="warning" %}
This section called only by `developer` address.
{% endhint %}

{% content-ref url="initial-setup/" %}
[initial-setup](initial-setup/)
{% endcontent-ref %}

### Call deploy of DEX

Initialization of new DEX separated into 2 stages because of gas transaction limits.&#x20;

The first stage deploys the contract and all lambdas except `dex_lambdas` (the heaviest lambdas by size) and charges QUIPU tokens but the contract has not started yet (frozen).&#x20;

The second stage should be called by caller address of the first stage and performs set of DEX lambdas to deployed DEX, unfreezes the contract, and call invest (as initial invest) of underlying tokens.

{% content-ref url="initialize-new-dex-flow/" %}
[initialize-new-dex-flow](initialize-new-dex-flow/)
{% endcontent-ref %}

### Deployed DEX

The link below describes the usage of deployed DEX contract and its storage.

{% content-ref url="deployed-from-factory-dex/" %}
[deployed-from-factory-dex](deployed-from-factory-dex/)
{% endcontent-ref %}

### Developer-only (admin) methods

As a developer, you could manage the dev fee rate, set the deploy price, and its burn percent. Also, the developer could add and remove addresses to the whitelist (for deploying new pools without charging QUIPU).

{% content-ref url="developer-methods/" %}
[developer-methods](developer-methods/)
{% endcontent-ref %}
