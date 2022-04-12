# default

An entrypoint for TEZ tokens receiving. After receiving, the contract swaps them for QUIPU tokens on [QuipuSwap DEX](https://quipuswap.com/swap/tez-KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb\_0) and generates the transaction for getting QUIPU tokens balance on this contract.

### Call parameters

An entrypoint doesn't accept any parameters.

{% hint style="danger" %}
Note: you need to pass positive TEZ/mutez amount to _**send()**_** ** method (see example below).
{% endhint %}

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const burnerAddress = "KT1...";
const mutezAmount = 100;
const burner = await tezos.contract.at(burnerAddress);
const operation = await burner.methods.default([]).send({ amount: mutezAmount, mutez: true });

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

An entrypoint doesn't throw any error.
