# set\_init\_function

Method for set DEX contract deployer function lambda.

Deployer function deploys new DEX contract to the blockchain with copied admin and token lambdas and charges deploy fee in QUIPU tokens. Part of fees stays inside contact reserves (`quipu_rewards`) and the other part goes to "burn address" - hardcoded zero-address to burn QUIPU tokens.

Input param type is `bytes`.

{% hint style="warning" %}
This contract method is called only by `developer` of that contract.
{% endhint %}
