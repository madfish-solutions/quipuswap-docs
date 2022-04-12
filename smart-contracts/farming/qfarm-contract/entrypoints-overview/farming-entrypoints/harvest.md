# harvest

An entrypoint that harvests (claims) user's rewards. Rewards are minted to the user and to the referrer (_**harvest\_fee**_).

### Call parameters

```pascaligo
type harvest_type       is [@layout:comb] record [
  fid                     : fid_type;
  rewards_receiver        : address;
]
```

| Field             | Type            | Description               |
| ----------------- | --------------- | ------------------------- |
| fid               | fid\_type (nat) | Farm's ID                 |
| rewards\_receiver | address         | Receiver of earned tokens |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const params = {
    fid: 1,
    rewards_receiver: "tz1.../KT1...",
};
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methodsObject.harvest(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
* `QFarm/timelock-is-not-finished` - timelock after last user's deposit (stake) is not finished.
