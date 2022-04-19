# set\_fees

An entrypoint that setups interface fee, swap fee, and auction fee that applies in time of each [_**swap**_](../dex-entrypoints/swap.md) or [_**flash\_swap**_](../dex-entrypoints/flash\_swap.md)**.** Also it setups a reward for withdrawing auction fee that applies in time of calling [_**withdraw\_auction\_fee**_](../dex-entrypoints/withdraw\_auction\_fee.md) entrypoint by any user.

### Call parameters

```pascaligo
type fees_t             is [@layout:comb] record [
  interface_fee           : nat;
  swap_fee                : nat;
  auction_fee             : nat;
  withdraw_fee_reward     : nat;
]
```

| Field                 | Type | Hint                            | Description                                                                                                                                                                   |
| --------------------- | ---- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| interface\_fee        | nat  | Float value multiplied by 1e+18 | Fee that goes to referrers or UI/UX providers                                                                                                                                 |
| swap\_fee             | nat  | Float value multiplied by 1e+18 | Fee that goes to the liquidity pool (for liquidity providers)                                                                                                                 |
| auction\_fee          | nat  | Float value multiplied by 1e+18 | Fee that goes to the [Auction](../../../auction-contract/) contract                                                                                                           |
| withdraw\_fee\_reward | nat  | Float value multiplied by 1e+18 | The % of the rewards that will be transferred to the transaction sender when he calls [_**withdraw\_auction\_fee**_](../dex-entrypoints/withdraw\_auction\_fee.md) entrypoint |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const interfaceFee = 0.05 * 10 ** 18; // 0.05%
const swapFee = 0.05 * 10 ** 18; // 0.05%
const auctionFee = 0.4 * 10 ** 18; // 0.4%
const withdrawFeeReward = 3 * 10 ** 18; // 3%
const dexCoreAddress = "KT1...";
const fees = {
    interface_fee: interfaceFee,
    swap_fee: swapFee,
    auction_fee: auctionFee,
    withdraw_fee_reward: withdrawFeeReward,
};
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methodsObject.set_fees(fees).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
