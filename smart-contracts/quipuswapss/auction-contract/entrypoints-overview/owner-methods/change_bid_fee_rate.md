# Change\_bid\_fee\_rate

This method is used to remove NFT minter.

### Call parameters

| Field               | Type | Description        |
| ------------------- | ---- | ------------------ |
| new\_bid\_fee\_rate | nat  | New bid fee amount |

### Usage

{% code title="🌮 Taquito" %}
```javascript
const nftAddress = "KT1...";
const newMinter = "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc";
const nftContract = await tezos.contract.at(nftAddress);
const operation = await nftContract.methods.remove_minter(newMinter).send();

await operation.confirmation();
```
{% endcode %}

### Post conditions

![](<../../../../../.gitbook/assets/image (12) (1).png>)

### Errors

`N/not-owner - sender` of the transaction is not current owner.
