# 📤 Divesting

Withdrawal actions contain 3 entrypoints that allow the user to withdraw underlying tokens by burning liquidity tokens.

* Balanced divest - classic removing liquidity without any additional fees.

{% content-ref url="divest.md" %}
[divest.md](divest.md)
{% endcontent-ref %}

* Imbalanced divest - allows to withdraw specific amount of underlying token(-s).

{% content-ref url="divest_imbalanced.md" %}
[divest\_imbalanced.md](divest\_imbalanced.md)
{% endcontent-ref %}

* Divest in one coin - allows to withdraw in one of underlying token by burning specific amount of shares.

{% content-ref url="divest_one_coin.md" %}
[divest\_one\_coin.md](divest\_one\_coin.md)
{% endcontent-ref %}

### Divest imbalance vs divest one

If you try to divest in imbalanced method you should pass **required** amount(-s) of output token(-s) and **maximum** of LP token (shares) to be burnt.

When you try to divest in one coin you should pass amount of shares to be burnt and **minimal amount** of token that you want to receive.

{% hint style="danger" %}
All of sent shares would be burnt when divest in one coin. Even if shares value greater than avaliable reserves of token.
{% endhint %}

In each way you would pay some fees to pool for imbalanced divest.

If you divest in balanced way, you wouldn’t pay any fees.
