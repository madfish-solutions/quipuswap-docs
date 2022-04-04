# Copy of Change\_owner

This method is used to change the contract ownership.

### Call parameters

| Field      | Type    | Description       |
| ---------- | ------- | ----------------- |
| new\_owner | address | New owner address |

### Usage

{% code title="🌮 Taquito" %}
```javascript
const nftAddress = "KT1...";
const newOwner = "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc";
const nftContract = await tezos.contract.at(nftAddress);
const operation = await nftContract.methods.change_owner(newOwner).send();

await operation.confirmation();
```
{% endcode %}

### Post conditions

![](<../../../../../.gitbook/assets/image (10) (1).png>)

### Errors

`N/not-owner - sender` of the transaction is not current owner.
