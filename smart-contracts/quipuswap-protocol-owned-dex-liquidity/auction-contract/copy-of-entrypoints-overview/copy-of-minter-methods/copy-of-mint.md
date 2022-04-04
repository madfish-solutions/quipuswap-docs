# Copy of Mint

This method is used to mint new NFT from current collection.

### Call parameters

| Field     | Type    | Description   |
| --------- | ------- | ------------- |
| recipient | address | NFT recipient |

### Usage

{% code title="🌮 Taquito" %}
```javascript
const nftAddress = "KT1...";
const recipient = "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc";
const nftContract = await tezos.contract.at(nftAddress);
const operation = await nftContract.methods.mint(recipient).send();

await operation.confirmation();
```
{% endcode %}

### Post conditions

![](<../../../../../.gitbook/assets/image (9).png>)

### Errors

`N/not-minter - sender` of the transaction is not minter.

`N/wrong-collection-id -` In this method, this error means that there is no collection to minting.
