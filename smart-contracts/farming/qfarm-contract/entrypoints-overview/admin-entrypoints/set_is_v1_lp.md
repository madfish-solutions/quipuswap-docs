# set\_is\_v1\_lp

An entrypoint that setups a new boolean flag: is QuipuSwap V1 LP token staked on the farm or not. Needs only in time when farm was deployed with incorrect `is_v1_lp` staked parameter.

### Call parameters

```pascaligo
type set_is_v1_lp_type  is [@layout:comb] record [
  fid                     : fid_type;
  is_v1_lp                : bool;

```

| Field      | Type            | Description                                              |
| ---------- | --------------- | -------------------------------------------------------- |
| fid        | fid\_type (nat) | Farm's ID                                                |
| is\_v1\_lp | bool            | Flag that indicates: QuipuSwap V1 LP token staked or not |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const params = {
    fid: 1,
    is_v1_lp: true, // or false
};
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methodsObject.set_is_v1_lp(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
