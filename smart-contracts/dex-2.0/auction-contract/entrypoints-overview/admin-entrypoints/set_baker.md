# set\_baker

An entrypoint that setups a new baker for whom all TEZ tokens on the contract will be delegated after setup. Also admin can remove a baker. For this he need to pass `None` as the call parameter.

### Call parameters

| Field | Type              | Description            |
| ----- | ----------------- | ---------------------- |
| baker | option(key\_hash) | A baker for delegation |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const auctionAddress = "KT1...";
const baker = "tz1..."; // or null, or undefined to remove a baker
const auction = await tezos.contract.at(auctionAddress);
const operation = await auction.methods.set_baker(baker).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
* operation also fails when the `option(key_hash)` parameter is not a registered delegate (standard Tezos error).
