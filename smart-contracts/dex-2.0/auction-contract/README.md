# ⚖ Auction contract

In time of each [_**swap**_](../dexcore-contract/entrypoints-overview/dex-entrypoints/swap.md) or [_**flash\_swap**_](../dexcore-contract/entrypoints-overview/dex-entrypoints/swap.md) operation [DexCore](../dexcore-contract/) contract collects _**auction\_fee**_. Anyone can call a method to send this fee to this Auction contract ([_**withdraw\_auction\_fee**_](../dexcore-contract/entrypoints-overview/dex-entrypoints/withdraw\_auction\_fee.md) entrypoint on [DexCore](../dexcore-contract/) contract) and earn a percentage of the money sent.

All the money that comes to this Auction contract is distributed into two funds: dev, which can be withdrawn by the administrator at any time, and public.

There are two types of tokens: some are whitelisted, others are not. All money of whitelisted tokens from the public fund can be withdrawn by the administrator of the contract.

All money of **NON** whitelisted tokens from the public fund can be bought at the auction. Anyone can start an auction with a fixed minimum bid in QUIPU tokens and try to buy any amount of any available token. A small percentage is removed from each bet and stored on the contract. The bid of the winner of the auction is burned, and he receives the tokens he staked on. The administrator can burn the accumulated QUIPU tokens from bets at any time.

Burning means that all QUIPU tokens are transferred to the `zero_address`.

{% hint style="info" %}
`zero_address` is the account address that no one has access to: [`tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg`](https://tzkt.io/tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg/operations/)``
{% endhint %}
