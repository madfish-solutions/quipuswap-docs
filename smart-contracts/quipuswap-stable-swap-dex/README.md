# QuipuSwap stable swap DEX

## About

Stable DEX, as a part of the growing QuipuSwap ecosystem, provides a platform for price-efficient and low-risk stablecoin or equal-price token trading. We intend to create a solution for the Tezos ecosystem akin to that Curve and Ellipsis have created for Ethereum and BSC, respectively.

{% embed url="https://github.com/madfish-solutions/quipuswap-stable-core" %}
Code of contracts
{% endembed %}

## Contracts overview

### Standalone

{% content-ref url="standalone-dex/" %}
[standalone-dex](standalone-dex/)
{% endcontent-ref %}

Is the all-in-one contract with a contract `admin` that allowed to add new DEX pools.&#x20;

{% content-ref url="standalone-dex/add-new-dex/" %}
[add-new-dex](standalone-dex/add-new-dex/)
{% endcontent-ref %}

Each pool stored in storage by `poolId` is an exchange between 2-4 tokens and has a corresponding LP token of FA2 standard with token ID = `poold`. Main DEX methods of each pool shown at

{% content-ref url="standalone-dex/dex-methods/" %}
[dex-methods](standalone-dex/dex-methods/)
{% endcontent-ref %}

Also, the standalone includes [developer-module](developer-module/ "mention") inside it (Admin =/= Developer).

### Factory

{% content-ref url="factory/" %}
[factory](factory/)
{% endcontent-ref %}

Allows use DaaS way to deploy new DEX pools for QUIPU fee and use own Stable Exchange with own params. For security reasons, each DEX pool is deployed as a separate contract.

{% content-ref url="factory/initialize-new-dex-flow/" %}
[initialize-new-dex-flow](factory/initialize-new-dex-flow/)
{% endcontent-ref %}

These deployed pools almost have the same logic as the standalone variant with a little difference - only one pool per contract. Each contract knows about factory, where located [developer-module](developer-module/ "mention").&#x20;

**`Developer`**, formally is the administrator of Factory. This address performs the initial setup of lambda methods

{% content-ref url="factory/initial-setup/" %}
[initial-setup](factory/initial-setup/)
{% endcontent-ref %}

&#x20;and some additional setters

{% content-ref url="factory/developer-methods/factory-management/factory-params/" %}
[factory-params](factory/developer-methods/factory-management/factory-params/)
{% endcontent-ref %}

### The main difference in implementations

In short, the difference is that

| Standalone pool                                                                             | Factory pool                                                                            |
| ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| each pool has own `poolId`, as known as token ID of pool's corresponding FA2 typed LP token | each pool LP token is an FA2 typed with token Id `0` and an unique address              |
| only administrator allowed to add new pools                                                 | everyone could start a new pool when paid gas fees and some deploy fee in QUIPU tokens. |
| contract owns developer params                                                              | pool calls factory views for developer params                                           |

#### Developer key values stay in the developer's hands.

Developer represents person or group that create and improve code of Standalone or Factory contract. This address allows to claim fee rewards and manage some values. More info about main developer setter/storage module is shown here

{% content-ref url="developer-module/" %}
[developer-module](developer-module/)
{% endcontent-ref %}

Additional values stored inside the implementation of specific contract - Factory or Standalone.

