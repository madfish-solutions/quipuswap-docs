# set\_auction

An entrypoint that setups a new **Auction** contract (see [Auction](../../../auction-contract/)).

### Call parameters

| Field   | Type    | Description                              |
| ------- | ------- | ---------------------------------------- |
| auction | address | An address of a new **Auction** contract |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const auctionAddress = "KT1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methods.set_auction(auctionAddress).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
