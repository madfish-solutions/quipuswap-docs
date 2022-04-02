# Add\_minter

This method is used to add NFT minter.

### Call parameters

| Field       | Type    | Description        |
| ----------- | ------- | ------------------ |
| new\_minter | address | New minter address |

### Usage

{% code title="🌮 Taquito" %}
```javascript
const nftAddress = "KT1...";
const newMinter = "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc";
const nftContract = await tezos.contract.at(nftAddress);
const operation = await nftContract.methods.add_minter(newMinter).send();

await operation.confirmation();
```
{% endcode %}

### Post conditions

![](<../../../../../.gitbook/assets/image (11) (1) (1).png>)

### Errors

`N/not-owner - sender` of the transaction is not current owner.
