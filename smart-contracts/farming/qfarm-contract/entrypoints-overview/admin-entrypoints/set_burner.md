# set\_burner

An entrypoint that setups a new **Burner** contract for burning QUIPU tokens exchanged on [QuipuSwap DEX](https://quipuswap.com/swap/tez-KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb\_0) using bakers rewards (see [Burner](../../../burner-contract/)).

### Call parameters

| Field  | Type    | Description                             |
| ------ | ------- | --------------------------------------- |
| burner | address | An address of a new **Burner** contract |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const burner = "KT1...";
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.set_burner(burner).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
