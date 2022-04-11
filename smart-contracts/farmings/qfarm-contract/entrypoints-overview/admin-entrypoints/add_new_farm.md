# add\_new\_farm

An entrypoint that adds a new farm with the specified parameters. Also setups share token default metadata.

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
  burn_reward             : nat;
]

type stake_params_type  is [@layout:comb] record [
  staked_token            : token_type;
  is_v1_lp                : bool;
]

type add_new_farm_type  is [@layout:comb] record [
  fees                    : fees_type;
  stake_params            : stake_params_type;
  token_info              : map(string, bytes);
  paused                  : bool;
  reward_per_second       : nat;
  timelock                : nat;
  start_time              : timestamp;
]
```

#### fees\_type

| Field           | Type | Hint                            | Description                                                                                                                                                          |
| --------------- | ---- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| harvest\_fee    | nat  | Float value multiplied by 1e+16 | Fee that applies in time of rewards claiming                                                                                                                         |
| withdrawal\_fee | nat  | Float value multiplied by 1e+16 | Fee that applies in time of withdrawing (unstaking) tokens only in farms with timelock                                                                               |
| burn\_reward    | nat  | Float value multiplied by 1e+16 | The % of the rewards that will be minted to the transaction sender when he calls [_**burn\_farm\_rewards**_](../other-entrypoints/burn\_farm\_rewards.md) entrypoint |

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
| paused              | bool                                                         | Flag that indicates: farm is paused or not         |
| reward\_per\_second | nat                                                          | Reward per second                                  |
| timelock            | nat                                                          | Timelock in seconds (0 for farms without timelock) |
| start\_time         | timestamp                                                    | Farm's start time                                  |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
import { MichelsonMap } from "@taquito/michelson-encoder";

const qFarmAddress = "KT1...";
const params = {
    fees: {
        harvest_fee: 0.05 * 10 ** 16, // 0.05%
        withdrawal_fee: 0.25 * 10 ** 16, // 0.25%
        burn_reward: 3 * 10 ** 16, // 3%
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
    paused: false, // or true
    reward_per_second: 1169098400000000,
    timelock: 0, // or positive number
    start_time: String(Math.ceil(Date.now() / 1000)),
};
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methodsObject.add_new_farm(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
