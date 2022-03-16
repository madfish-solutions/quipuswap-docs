# 🟠 Add new dex

This page describes creation of new DEX pool.&#x20;

{% hint style="warning" %}
These contract methods are called only by `admin` of that contract.
{% endhint %}

Creation of pool consist of some parameters for seeting up DEX config.

#### a\_constant

Constant A used for manipulating with swap function. As larger the value of A, as more the function tends to be constant sum invariant. This constant is stored inside the contact as  $$A_{storage} = A * n^{n-1}$$ where $$2 \le n \le 4$$ - number of DEX underlying tokens. You could read more about this constant at Curve [whitepaper](https://curve.fi/files/stableswap-paper.pdf) and an explanation of Curve formulas.

{% embed url="https://miguelmota.com/blog/understanding-stableswap-curve" %}
An explanation of Curve formulas
{% endembed %}

#### input\_tokens

This param is a set of FA12/FA2 tokens that would be traded on DEX. `Set` type in Tezos contract is the sorted list of unique values, so you must keep in mind that for setting up `tokens_info` and when calling DEX.

#### tokens\_info

Token Info contains initial data for [#token-information-type-pool-underlying-token-info](../storage-and-types-overview.md#token-information-type-pool-underlying-token-info "mention").&#x20;

{% content-ref url="add_pool.md" %}
[add\_pool.md](add\_pool.md)
{% endcontent-ref %}

### Token info setting

When you want to initialise pool, you should setup initial `reserves`, `rate` and `precision_multiplier` in correct way:

> Let 4 `TBC` = 2 `TXZ` = 1 `TEH` (from example)

Then calculate $$LCM$$ of these ratios $$= 4$$

Token info for `TBC`

> `precision_multiplier` - $$10^{decimal_{LP} - decimal_{TBC}}$$
>
> `rate` - $$10^{decimal_{LP}} * 10^{decimal_{LP} - decimal_{TBC}} * (ratio_{TBC}/LCM)$$
>
> `reserves` - $$N * 10^{decimal_{TBC}} * ratio_{TBC}$$

Token info for `TXZ`

> `precision_multiplier` - $$10^{decimal_{LP} - decimal_{TXZ}}$$
>
> `rate` - $$10^{decimal_{LP}} * 10^{decimal_{LP} - decimal_{TXZ}} * (ratio_{TXZ}/LCM)$$
>
> `reserves` - $$N * 10^{decimal_{TXZ}} * ratio_{TXZ}$$

Token info for `TEH`

> `precision_multiplier` - $$10^{decimal_{LP} - decimal_{TEH}}$$
>
> `rate` - $$10^{decimal_{LP}} * 10^{decimal_{LP} - decimal_{TEH}} * (ratio_{TEH}/LCM)$$
>
> `reserves` - $$N * 10^{decimal_{TEH}} * ratio_{TEH}$$

Then you should receive $$LPT = 10^{decimal_{LP}} * LCM * tokensCount$$ LP tokens.

Details of how to calculate values are in this table. (You can copy and play with this sheet)

{% embed url="https://docs.google.com/spreadsheets/d/16sfuK6o8mWxOtG4pagxvRiUoswmA4SUO4aFzDa8yTD8/edit?usp=sharing" %}
Stable exchange with switching of amount of tokens
{% endembed %}
