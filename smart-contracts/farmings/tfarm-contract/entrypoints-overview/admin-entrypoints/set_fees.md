# set\_fees

An entrypoint that setups fee for the specified farm. Also can setup fees for a group of farms in one transaction.

### Call parameters

```pascaligo
type fees_type          is [@layout:comb] record [
  harvest_fee             : nat;
  withdrawal_fee          : nat;
]

type set_fee_type       is [@layout:comb] record [
  fid                     : fid_type;
  fees                    : fees_type;
]

type set_fees_type      is list(set_fee_type)
```

#### fees\_type

| Field           | Type | Hint                            | Description                                                                                                                      |
| --------------- | ---- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| harvest\_fee    | nat  | Float value multiplied by 1e+16 | Fee that applies in time of rewards claiming                                                                                     |
| withdrawal\_fee | nat  | Float value multiplied by 1e+16 | Fee that applies in time of withdrawing (unstaking) tokens only in farms with timelock. Applies only in case of early withdrawal |

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
const tFarmAddress = "KT1...";
const fees = [
    {
        fid: farmId,
        fees: {
            harvest_fee: harvestFee,
            withdrawal_fee: withdrawalFee,
        },
    },
    ...
];
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methods.set_fees(fees).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
