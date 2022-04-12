# pause\_farms

An entrypoint that updates users' rewards and pauses/unpauses the specified farm. Can pause/unpause a group of farms in one transaction. Paused farms can't accept deposits (stakes).

### Call parameters

```pascaligo
type pause_farm_type    is [@layout:comb] record [
  fid                     : fid_type;
  pause                   : bool;
]

type pause_farms_type   is list(pause_farm_type)
```

| Field | Type            | Description                                  |
| ----- | --------------- | -------------------------------------------- |
| fid   | fid\_type (nat) | Farm's ID                                    |
| pause | bool            | Flag that indicates: pause or unpause a farm |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const tFarmAddress = "KT1...";
const params = [
    {
        fid: 1,
        pause: true, // or false to unpause the farm
    },
    ...
];
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methods.pause_farms(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
