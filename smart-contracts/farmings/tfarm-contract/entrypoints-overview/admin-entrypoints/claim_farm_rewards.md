# claim\_farm\_rewards

An entrypoint that claims the specified farm rewards. All rewards will be transferred to the admin. Rewards are accrued to the farm for the funds that were staked from a farm's name as a withdrawal commission.

### Call parameters

```pascaligo
type claim_farm_type    is nat // Farm's ID
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const tFarmAddress = "KT1...";
const farmId = 1;
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methods.claim_farm_rewards(farmId).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
