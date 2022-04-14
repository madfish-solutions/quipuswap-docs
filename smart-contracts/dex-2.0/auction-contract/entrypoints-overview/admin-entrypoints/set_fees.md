# set\_fees

An entrypoint that setups dev and bid fees.

### Call parameters

```pascaligo
type fees_t             is [@layout:comb] record [
  dev_fee_f               : nat;
  bid_fee_f               : nat;
]
```

| Field       | Type | Hint                            | Description                                                                                                                                     |
| ----------- | ---- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| dev\_fee\_f | nat  | Float value multiplied by 1e+18 | Fee that goes to the devs fund and can be [withdrawn](withdraw\_dev\_fee.md) by an administrator                                                |
| bid\_fee\_f | nat  | Float value multiplied by 1e+18 | Fee in [QuipuSwap Governance token](https://tzkt.io/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/operations/) that applies on each bid for all auctions |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const devFeeF = 0.25 * 10 ** 18; // 0.25%
const bidFeeF = 0.5 * 10 ** 18; // 0.5%
const auctionAddress = "KT1...";
const fees = {
    dev_fee_f: devFeeF,
    bid_fee_f: bidFeeF,
};
const auction = await tezos.contract.at(auctionAddress);
const operation = await dexCore.methodsObject.set_fees(fees).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
