# deposit

An entrypoint that deposits (stakes) tokens. In time of every deposit it claims user's rewards if timelock is finished (only for farms with timelock) or in farms without timelock it just claims user's rewards. In the case of claiming, rewards are minted to the user and to the referrer (_**harvest\_fee**_). Also setups a referrer for a user, votes for a user's baker if the QuipuSwap V1 TOK/TEZ LP token is deposited (staked).

### Call parameters

```pascaligo
type deposit_type       is [@layout:comb] record [
  fid                     : fid_type;
  amt                     : nat;
  referrer                : option(address);
  rewards_receiver        : address;
  candidate               : option(key_hash);
]
```

| Field             | Type              | Description                                                           |
| ----------------- | ----------------- | --------------------------------------------------------------------- |
| fid               | fid\_type (nat)   | Farm's ID                                                             |
| amt               | nat               | Amount of tokens to deposit                                           |
| referrer          | option(address)   | User's referrer                                                       |
| rewards\_receiver | address           | Receiver of earned tokens                                             |
| candidate         | option(key\_hash) | The baker for voting (only for QuipuSwap V1 TOK/TEZ LP staked tokens) |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const params = {
    fid: 1,
    amt: 100,
    referrer: "tz1.../KT1...", // or null
    rewards_receiver: "tz1.../KT1...",
    candidate: "tz1...", // or null
};
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methodsObject.deposit(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
* `QFarm/farm-is-paused` - farm is paused by an administrator.
* `QFarm/can-not-refer-yourself` - user is trying to refer himself.
* `QFarm/baker-is-required` - `baker` parameter is required (not optional) for QuipuSwap V1 TOK/TEZ LP staked tokens.
* `QFarm/baker-is-banned` - `baker` from the parameters is banned by an administrator.
