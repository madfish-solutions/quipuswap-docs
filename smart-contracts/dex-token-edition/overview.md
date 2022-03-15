# Overview



Token-friendly AMM is the second automated liquidity protocol version implemented by the Quipuswap. Just as the initial exchange, it aims to empower decentralization, censorship resistance, and security.

The liquidity pool, or pair, is the core atom of the system. Despite the fact that the pool is just an abstraction inside the single contract and not the separate contract instance, each pool is managed separately, and such architecture enables the seamless multihop swaps.

Anyone can become a liquidity provider (LP) for a pool by depositing an equivalent value of each underlying token in return for LP tokens. The tokens represent the user’s share in the pool and can be withdrawn for the underlying assets at any time.

If the pair for certain FA1.2 or/and FA2 tokens doesn’t exist or all the liquidity was withdrawn, anyone can launch it by providing the initial liquidity.

AMM token edition is the automated market maker engine. It follows the exchange path provided by the caller and executes the exchanges, ensuring that the final output amount matches the user’s expectations. Under the hood, each swap is performed according to the constant product formula `x * y = k` which actually means that the product of tokens reserves should be the same before and after the swap.&#x20;

In practice, Quipuswap applies a 0.30% fee to trades, which is added to reserves. As a result, each trade actually increases `k`, and thus reserves under the same amount of shares increase, allowing the LP providers to earn.

**The core difference from the Quipuswap v2:**

* token/token pools are supported;
* multihop pools are supported;
* all actions have a deadline;
* all the pools and reserves are stored on a single contract.

As mentioned, the solution consists of a single contract that acts as a pools register and automated market maker engine.
