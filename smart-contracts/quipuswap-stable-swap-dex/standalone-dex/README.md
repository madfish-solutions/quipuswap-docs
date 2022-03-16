# 🏠 Standalone DEX

This all-in-one contract, managed by `admin`. Each deployed DEX is stored inside the current contract and has its own FA2 token. Access to a specific DEX, implemented by pool ID. This ID is an also LP token ID. Every token metadata is managed by any of the manager's addresses.

### Storage

Contract storage has a complicated structure all info about storage is collected on the page below.

{% content-ref url="storage-and-types-overview.md" %}
[storage-and-types-overview.md](storage-and-types-overview.md)
{% endcontent-ref %}

### Core methods

Main methods of DEX, that are able to use by anyone. These methods include investing, swapping, and divesting. Also, there are additional methods for staking QUIPU tokens for earning additional rewards and claiming referral rewards.

{% content-ref url="dex-methods/" %}
[dex-methods](dex-methods/)
{% endcontent-ref %}

### Developer-only methods

The developer section contains [developer-module](../developer-module/ "mention") entrypoints and additional methods for claiming developer rewards.

{% hint style="warning" %}
These entrypoints should be called only by `developer` address.&#x20;
{% endhint %}

{% content-ref url="developer-methods/" %}
[developer-methods](developer-methods/)
{% endcontent-ref %}

### Admin methods

{% hint style="warning" %}
These entrypoints should be called only by `admin` address.&#x20;
{% endhint %}

The next section is about entrypoints for managing fees, "A" constant change, editing manager list, and changing an admin address.

{% content-ref url="admin-methods/" %}
[admin-methods](admin-methods/)
{% endcontent-ref %}

#### Initial setup of contract

These methods should be used **before** global usage of contract. Entrypoints set lambda-functions to its corresponding indexes inside related big maps.

{% content-ref url="initialization/" %}
[initialization](initialization/)
{% endcontent-ref %}

#### Create a new DEX pool

Creating a new DEX pool in the standalone variant is an admin function. So only the admin can create a new pool. Admin should approve the needed amount of tokens before calling this method because call includes transfer selected tokens to contract.

{% content-ref url="add-new-dex/" %}
[add-new-dex](add-new-dex/)
{% endcontent-ref %}

### Examples hint

{% hint style="info" %}
All examples use LP token with `decimals` of $$18$$ ↔ `precision` constant as $$10^{18}$$ and 3 "abstract" tokens `TBC`, `TXZ`, `TEH` that have ratios $$4:2:1$$ respectively.
{% endhint %}
