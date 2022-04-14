# set\_auction\_duration

An entrypoint that setups default auction duration. The duration for previously created auctions will not change. The changes will only affect auctions that will be created after the change of the duration.

### Call parameters

| Field             | Type | Description                        |
| ----------------- | ---- | ---------------------------------- |
| auction\_duration | nat  | New default duration of an auction |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const auctionAddress = "KT1...";
const auctionDuration = 86400; // 24 hours
const auction = await tezos.contract.at(auctionAddress);
const operation = await auction.methods.set_auction_duration(auctionDuration).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
