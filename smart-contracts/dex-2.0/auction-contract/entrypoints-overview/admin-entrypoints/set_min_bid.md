# set\_min\_bid

An entrypoint that setups a minimum bid that will be used to check user's first bid in time of auction launch.

### Call parameters

| Field    | Type | Description     |
| -------- | ---- | --------------- |
| min\_bid | nat  | New minimum bid |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const auctionAddress = "KT1...";
const minBid = 100;
const auction = await tezos.contract.at(auctionAddress);
const operation = await auction.methods.set_min_bid(minBid).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
