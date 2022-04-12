# set\_reward\_per\_second

An entrypoint that setups a new reward per second in QUIPU tokens for the specified farm. Can update rewards per second for a group of farms in one transaction.

### Call parameters

```pascaligo
type rew_per_sec_type   is [@layout:comb] record [
  fid                     : fid_type;
  reward_per_second       : nat;
]

type set_rew_p_sec_type is list(rew_per_sec_type)
```

| Field               | Type            | Description           |
| ------------------- | --------------- | --------------------- |
| fid                 | fid\_type (nat) | Farm's ID             |
| reward\_per\_second | nat             | New reward per second |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const farmId = 1;
const rewardPerSecond = 100;
const qFarmAddress = "KT1...";
const params = [
    {
        fid: farmId,
        reward_per_second: rewardPerSecond,
    },
    ...
];
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.set_reward_per_second(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
