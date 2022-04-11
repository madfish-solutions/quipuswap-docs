# add\_new\_farm

An entrypoint that adds a new farm with the specified parameters. Also setups share token default metadata. Required amount of reward token will be transferred from an admin to the contract (allowance is required).

### Call parameters

```pascaligo
type fa12_type          is address

type fa2_type           is [@layout:comb] record [
  token                   : address;
  id                      : token_id_type;
]

type token_type         is
  FA12                    of fa12_type
| FA2                     of fa2_type

type fees_type          is [@layout:comb] record [
  harvest_fee             : nat;
  withdrawal_fee          : nat;
]

type stake_params_type  is [@layout:comb] record [
  staked_token            : token_type;
  is_v1_lp                : bool;
]

type add_new_farm_type  is [@layout:comb] record [
  fees                    : fees_type;
  stake_params            : stake_params_type;
  token_info              : map(string, bytes);
  reward_token            : token_type;
  paused                  : bool;
  timelock                : nat;
  start_time              : timestamp;
  end_time                : timestamp;
  reward_per_second       : nat;
]
```

#### fees\_type

| Field           | Type | Hint                            | Description                                                                            |
| --------------- | ---- | ------------------------------- | -------------------------------------------------------------------------------------- |
| harvest\_fee    | nat  | Float value multiplied by 1e+16 | Fee that applies in time of rewards claiming                                           |
| withdrawal\_fee | nat  | Float value multiplied by 1e+16 | Fee that applies in time of withdrawing (unstaking) tokens only in farms with timelock |

#### stake\_params\_type

| Field         | Type        | Description                                              |
| ------------- | ----------- | -------------------------------------------------------- |
| staked\_token | token\_type | FA1.2/FA2 staked token                                   |
| is\_v1\_lp    | bool        | Flag that indicates: QuipuSwap V1 LP token staked or not |

#### add\_new\_farm\_type

| Field               | Type                                                         | Description                                        |
| ------------------- | ------------------------------------------------------------ | -------------------------------------------------- |
| fees                | [fees\_type](add\_new\_farm.md#fees\_type)                   | Fees that applies to the farming                   |
| stake\_params       | [stake\_params\_type](add\_new\_farm.md#stake\_params\_type) | Staking parameters                                 |
| token\_info         | map(string, bytes)                                           | Mapping of token's keys to token's info            |
| reward\_token       | token\_type                                                  | FA1.2/FA2 reward token                             |
| paused              | bool                                                         | Flag that indicates: farm is paused or not         |
| timelock            | nat                                                          | Timelock in seconds (0 for farms without timelock) |
| start\_time         | timestamp                                                    | Farm's start time                                  |
| end\_time           | timestamp                                                    | Farm's end time                                    |
| reward\_per\_second | nat                                                          | Reward per second                                  |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
import { MichelsonMap } from "@taquito/michelson-encoder";

const tFarmAddress = "KT1...";
const lifetime = 10510000; // ~4 months
const params = {
    fees: {
        harvest_fee: 0.05 * 10 ** 16, // 0.05%
        withdrawal_fee: 0.25 * 10 ** 16, // 0.25%
    },
    stake_params: {
        staked_token: {
            fA2: {
                token: "KT1...",
                id: 0,
            },
        },
        is_v1_lp: true, // or false
    },
    token_info: MichelsonMap.fromLiteral({
        name: Buffer.from("wWBTC/TEZ FA2 Staking Share").toString("hex"),
        symbol: Buffer.from("QSHR").toString("hex"),
        decimals: Buffer.from("6").toString("hex"),
    }),
    reward_token: {
      fA12: "KT1...",
    },
    paused: false, // or true
    timelock: 0, // or positive number
    start_time: String(Math.ceil(Date.now() / 1000)),
    end_time: String(Math.floor(Date.now() / 1000) + lifetime + 1),
    reward_per_second: 1169098400000000,
};
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methodsObject.add_new_farm(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
* `TFarm/wrong-end-time` - end time of a farming is less that or equal to start time.
* `TFarm/wrong-timelock` - timelock is greater than farming's lifetime.
