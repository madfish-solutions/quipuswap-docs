# 🟠 Initialize new DEX flow

Deploy and initialization of DEX pool from factory performs in 2 steps. This is required because of the complexity of the contract itself and the size of stored lambda functions in it, so one-operation deployment exceeds gas limits.

### Step 1

{% hint style="warning" %}
QUIPU token should be approved (updated operators) before calling this method.
{% endhint %}

In first step, the contract deploys the main body of DEX, with copied admin and token lambdas and "frozen" flag, and charges QUIPU tokens as deploy fees, if the sender is not whitelisted.

{% content-ref url="add_pool.md" %}
[add\_pool.md](add\_pool.md)
{% endcontent-ref %}

### Step 2

{% hint style="warning" %}
Underlying tokens should be approved (updated operators) before calling this method.
{% endhint %}

Step two do three operations: copy dex lambdas (as largest by size), "unfreezes" DEX, and call invest with balanced values of all underlying tokens. As the DEX pool contract had not received any investments yet, this investment is initial and equal to investing when performed [add\_pool.md](../../standalone-dex/add-new-dex/add\_pool.md "mention")(Standalone version).

{% content-ref url="start_dex.md" %}
[start\_dex.md](start\_dex.md)
{% endcontent-ref %}
