# burn\_farm\_rewards

An entrypoint that claims and burns the specified farm rewards (they will be minted to the `zero_address`). Transaction sender receives minted to him burn rewards (this is the % that is specified by an admin in [burn\_rewards](../admin-entrypoints/set\_fees.md) fee). Rewards are accrued to the farm for the funds that were staked from a farm's name as a withdrawal commission.

{% hint style="info" %}
`zero_address` is the account address that no one has access to: [`tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg`](https://tzkt.io/tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg/operations/)``
{% endhint %}

### Call parameters

```pascaligo
type burn_farm_rew_type is nat // Farm's ID
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const farmId = 1;
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.burn_farm_rewards(farmId).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
