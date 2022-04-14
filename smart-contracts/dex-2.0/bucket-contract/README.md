# 🧺 Bucket contract

Bucket contract is an auxiliary contract that is responsible for storing TEZ tokens from TOK/TEZ liquidity pools (pairs). This contract is deployed for every TOK/TEZ pair and can't be changed. In time of exchange launch or liquidity investment TEZ tokens from [DexCore](../dexcore-contract/) contract is transferred to this contract. In time of liquidity divestment TEZ tokens returns to [DexCore](../dexcore-contract/) contract.

Bucket contract supports voting for bakers. In time of voting all TEZ tokens will be delegated to the best baker with a majority of votes. Also this baker can be changed during another vote operation.

The selected baker starts giving out baker's rewards that each user can claim (withdraw) at any time according to the number of votes that were given to the baker.

{% hint style="warning" %}
Baker can be banned by an administrator of [DexCore](../dexcore-contract/) contract. Because of this [_**vote**_](entrypoints-overview/vote.md) operation can fail.
{% endhint %}

{% hint style="danger" %}
Almost all entrypoints on Bucket contract can be called only by [DexCore](../dexcore-contract/) contract.
{% endhint %}
