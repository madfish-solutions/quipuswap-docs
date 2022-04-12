# set\_proxy\_minter

An entrypoint that setups a new **ProxyMinter** contract for minting QUIPU reward tokens for those who staked their tokens in farmings (see [ProxyMinter](../../../proxyminter-contract/)).

### Call parameters

| Field         | Type    | Description                                  |
| ------------- | ------- | -------------------------------------------- |
| proxy\_minter | address | An address of a new **ProxyMinter** contract |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const proxyMinter = "KT1...";
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.set_proxy_minter(proxyMinter).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
