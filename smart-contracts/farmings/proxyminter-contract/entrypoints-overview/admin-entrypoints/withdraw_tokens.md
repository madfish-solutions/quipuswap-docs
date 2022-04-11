# withdraw\_tokens

Withdraws specified QUIPU tokens amount minted to this contract in the result of calling QUIPU token's contract [_**mint\_gov\_token**_](https://better-call.dev/mainnet/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/interact?entrypoint=mint\_gov\_token) entrypoint by other minters (see QUIPU token documentation for detailed explanation).

### Call parameters

| Field  | Type | Description                            |
| ------ | ---- | -------------------------------------- |
| amount | nat  | Number of QUIPU tokens for withdrawing |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const proxyMinterAddress = "KT1...";
const amount = 100;
const proxyMinter = await tezos.contract.at(proxyMinterAddress);
const operation = await proxyMinter.methods.withdraw_tokens(amount).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
