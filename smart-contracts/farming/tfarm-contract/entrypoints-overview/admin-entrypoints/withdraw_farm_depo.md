# withdraw\_farm\_depo

An entrypoint that withdraws the specified by an admin value staked from farm's name. Votes for the farm's preferred baker if the farm supports LP tokens. If the farm does not have a preferred baker, the current delegated will be chosen as the preferred baker. Rewards are not claimed (use [claim\_farm\_rewards](claim\_farm\_rewards.md) entrypoint for this purpose)

### Call parameters

```pascaligo
type withdraw_farm_type is [@layout:comb] record [
  fid                     : fid_type;
  amt                     : nat;
]
```

| Field | Type            | Description                            |
| ----- | --------------- | -------------------------------------- |
| fid   | fid\_type (nat) | Farm's ID                              |
| amt   | nat             | Amount of tokens to withdraw (unstake) |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const tFarmAddress = "KT1...";
const params = {
    fid: 1,
    amt: 100,
};
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methodsObject.withdraw_farm_depo(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
* `QSystem/balance-too-low` - staked by farm tokens amount is less than amount parameter passed by an admin.
