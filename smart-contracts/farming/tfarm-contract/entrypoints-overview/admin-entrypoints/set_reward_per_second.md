# set\_reward\_per\_second

An entrypoint that setups a new reward per second for the specified farm.&#x20;

In case, when new reward per second is greater that previous, the missing number of reward tokens will be withdrawn from the admin account (allowance is required). When new reward per second is less than previous, extra tokens will be sent to the admin.

### Call parameters

```pascaligo
type set_rps_type       is [@layout:comb] record [
  fid                     : fid_type;
  reward_per_second       : nat;
]
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
const tFarmAddress = "KT1...";
const params = {
    fid: farmId,
    reward_per_second: rewardPerSecond,
};
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methods.set_reward_per_second(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
* `TFarm/farm-work-time-is-finished` - farming already finished it's working period.
* `TFarm/wrong-reward-per-second` - new reward per second is equal to the previous reward per second.
