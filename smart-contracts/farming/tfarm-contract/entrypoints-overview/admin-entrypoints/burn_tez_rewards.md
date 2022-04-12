# burn\_tez\_rewards

An entrypoint that withdraws bakers rewards from TOK/TEZ QuipuSwap liquidity pool to [Burner](../../../burner-contract/) contract. All rewards will be exchanged for QUIPU Governance tokens and burned.

### Call parameters

```pascaligo
type burn_tez_rew_type  is nat // Farm's ID
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const tFarmAddress = "KT1...";
const farmId = 1;
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methods.burn_tez_rewards(farmId).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
* `QSystem/not-LP-farm` - staked token is not QuipuSwap V1 TOK/TEZ LP token.
