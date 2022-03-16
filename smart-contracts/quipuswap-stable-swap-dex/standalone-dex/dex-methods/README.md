---
description: The core entrypoints
---

# 🔵 DEX methods

### Investing

Any user could invest their own liquidity to contract and receive Liquidity Pool Token (LPT). LPT allows earning interest from [#swapping](./#swapping "mention")and imbalanced invests/divests.&#x20;

#### Balanced invest

If user performs investment in corresponding ratios (example from [#examples-hint](../#examples-hint "mention") \[4 `TBC`; 2 `TXZ`; 1 `TEH`] is balanced input), it is expected to no additional fees are charged.

#### Imbalanced invest

If there is any LPT already exists, and invest is imbalanced (example from [#examples-hint](../#examples-hint "mention") \[1 `TBC`; 2 `TXZ`; 1 `TEH`] and \[1 `TXZ`] and \[8 `TXZ`; 4 `TEH`] is all imbalanced inputs) the additional fee charged for balancing pool reserves.

More info about invest entrypoint written out on the corresponding page.

{% content-ref url="invest.md" %}
[invest.md](invest.md)
{% endcontent-ref %}

### Swapping&#x20;

The main idea of DEX is to swap between different liquidity entries. This contract used swap math, which tried to keep math calculations as close as possible to [Curve](https://curve.fi) math. Each swap has a 0.05% fee that goes to liquidity providers (this part of the reward stays in liquidity pool), QUIPU pool stakers (if no one had staked yet, this part of the fee goes to liquidity providers), referral (if not provided goes to default referral address), and to the developer.

{% content-ref url="swap.md" %}
[swap.md](swap.md)
{% endcontent-ref %}

### Divesting

The liquidity provider could take back his liquidity by performing divest operation. The provider could choose a more convenient divest method from 3 variants: balanced/imbalanced/in one coin. Info about the difference of variants described at Divesting page.

{% content-ref url="divesting/" %}
[divesting](divesting/)
{% endcontent-ref %}

### Additional interest

Participators of  DEX pools are allowed to earn additional rewards as referrals or by staking QUIPU tokens. For more information about earning rewards in this way, follow the page under this text.

{% content-ref url="dex-rewards/" %}
[dex-rewards](dex-rewards/)
{% endcontent-ref %}
