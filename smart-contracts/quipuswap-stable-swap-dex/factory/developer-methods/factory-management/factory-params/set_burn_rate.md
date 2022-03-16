# set\_burn\_rate

{% hint style="warning" %}
This contract method is called only by `developer` of that contract.
{% endhint %}

This method sets which percent of the deployment price will be sent to a zero address (burned).

Accepts `nat` value - percent of price to burn multiplied by `100_0000n`.
