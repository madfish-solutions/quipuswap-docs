# withdraw

An entrypoint that withdraws (unstakes) tokens. In time of every withdraw it claims user's rewards if timelock is finished (only for farms with timelock) and burns user's rewards if timelock is not finished (only for farms with timelock). In farms without timelock it just claims the rewards. In the case of claiming, rewards are minted to the user and to the referrer (_**harvest\_fee**_). Also it takes a commission in staked tokens on withdrawal (_**withdrawal\_fee**_) if timelock is not finished (only for farms with timelock) and takes this commission from the farm's name. At the end it revotes for a baker if the farm supports QuipuSwap V1 TOK/TEZ LP tokens.

### Call parameter

```pascaligo
type withdraw_type      is [@layout:comb] record [
  fid                     : fid_type;
  amt                     : nat;
  receiver                : address;
  rewards_receiver        : address;
]
```

| Field             | Type            | Description                  |
| ----------------- | --------------- | ---------------------------- |
| fid               | fid\_type (nat) | Farm's ID                    |
| amt               | nat             | Amount of tokens to withdraw |
| receiver          | address         | Receiver of unstaked tokens  |
| rewards\_receiver | address         | Receiver of earned tokens    |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const params = {
    fid: 1,
    amt: 100,
    receiver: "tz1.../KT1...",
    rewards_receiver: "tz1.../KT1...",
};
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methodsObject.withdraw(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
* `QFarm/balance-too-low` - user's staked balance too low.
