# set\_fees

An entrypoint that setups fee for the specified farm. Also can setup fees for a group of farms in one transaction.

### Call parameters

```pascaligo
type fees_type          is [@layout:comb] record [
  harvest_fee             : nat;
  withdrawal_fee          : nat;
  burn_reward             : nat;
]

type set_fee_type       is [@layout:comb] record [
  fid                     : fid_type;
  fees                    : fees_type;
]

type set_fees_type      is list(set_fee_type)
```

#### fees\_type

| Field           | Type | Hint                            | Description                                                                                                                                                          |
| --------------- | ---- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| harvest\_fee    | nat  | Float value multiplied by 1e+16 | Fee that applies in time of rewards claiming                                                                                                                         |
| withdrawal\_fee | nat  | Float value multiplied by 1e+16 | Fee that applies in time of withdrawing (unstaking) tokens only in farms with timelock. Applies only in case of early withdrawal                                     |
| burn\_reward    | nat  | Float value multiplied by 1e+16 | The % of the rewards that will be minted to the transaction sender when he calls [_**burn\_farm\_rewards**_](../other-entrypoints/burn\_farm\_rewards.md) entrypoint |

#### set\_fee\_type

| Field | Type                                  | Description                      |
| ----- | ------------------------------------- | -------------------------------- |
| fid   | fid\_type (nat)                       | Farm's ID                        |
| fees  | [fees\_type](set\_fees.md#fees\_type) | Fees that applies to the farming |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const farmId = 1;
const harvestFee = 0.05 * 10 ** 16; // 0.05%
const withdrawalFee = 0.25 * 10 ** 16; // 0.25%
const burnReward = 3 * 10 ** 16; // 3%
const qFarmAddress = "KT1...";
const fees = [
    {
        fid: farmId,
        fees: {
            harvest_fee: harvestFee,
            withdrawal_fee: withdrawalFee,
            burn_reward: burnReward,
        },
    },
    ...
];
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.set_fees(fees).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
