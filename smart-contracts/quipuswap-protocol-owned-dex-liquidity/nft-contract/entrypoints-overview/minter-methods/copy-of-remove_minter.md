# Copy of Remove\_minter

This method is used to remove NFT minter.

### Call parameters

| Field  | Type    | Description                     |
| ------ | ------- | ------------------------------- |
| minter | address | Address of minter to be deleted |

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

![](<../../../../../.gitbook/assets/image (12).png>)

### Errors

`N/not-owner - sender` of the transaction is not current owner.
