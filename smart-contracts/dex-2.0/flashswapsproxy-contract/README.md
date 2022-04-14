# ⚙ FlashSwapsProxy contract

This is a helper contract. It is only needed in case of [flash\_swap](../dexcore-contract/entrypoints-overview/dex-entrypoints/flash\_swap.md) entrypoint call. It accepts a user's lambda from [_**DexCore**_](../dexcore-contract/) contract and executes it.

This implementation is due to the fact that users' lambdas can be malicious for a [_**DexCore**_](../dexcore-contract/) contract. And to avoid this, the execution of the users' lambdas is transferred to this _**FlashSwapProxy**_ contract.
