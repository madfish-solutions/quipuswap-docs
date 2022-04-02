# Transfer

This method is used to transfer NFT.

{% hint style="info" %}
In order for the transfer to be performed by a trusted operator, you must first call the Update\_operators.
{% endhint %}

### Call parameters

![](<../../../../../.gitbook/assets/image (5).png>)

| Field               | Type                                                       | Description   |
| ------------------- | ---------------------------------------------------------- | ------------- |
| transfer\_params\_t | list([transfer\_param\_t](transfer.md#transfer\_param\_t)) | NFT recipient |

### transfer\_param\_t

| Field  | Type                                                                                       | Description                             |
| ------ | ------------------------------------------------------------------------------------------ | --------------------------------------- |
| from\_ | <mark style="color:red;">address</mark>                                                    | Account from which the transfer is made |
| txs    | <mark style="color:yellow;">list</mark>([transfer\_destination\_t](transfer.md#undefined)) | List with transactions                  |
|        |                                                                                            |                                         |

### transfer\_destination\_t

| Field     | Types                                   | Description                       |
| --------- | --------------------------------------- | --------------------------------- |
| to\_      | <mark style="color:red;">address</mark> | Transfer recipient                |
| token\_id | <mark style="color:green;">nat</mark>   | ID of the token to be transferred |
| amount    | <mark style="color:green;">nat</mark>   | Transfer amount                   |

### Usage

{% code title="🌮 Taquito" %}
```javascript
const nftAddress = "KT1...";
const from = "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc"
const recipient = "tz1gKYy8uwdBHp9iw1PNiH7AJmzsvcVtmpwR";
const nftContract = await Tezos.contract.at(nftAddress);
const operation = await nftContract.methods.transfer([
  {
    from_: from,
    txs: [{ to_: recipient, token_id: 0, amount: 1 }],
  }]).send()

await operation.confirmation();
```
{% endcode %}

### Post conditions

![](<../../../../../.gitbook/assets/image (11) (1).png>)

```json
[
  {
    bigmap: 219664,
    path: "ledger",
    action: "update_key",
    content: {
      hash: "exprut9brcqmzR6Yd3G6FnE5CPMPsF5YUTa8YgmykaoPQDvRVqz8nF",
      key: {
        nat: "0",
        address: "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc",
      },
      value: "0",
    },
  },
  {
    bigmap: 219664,
    path: "ledger",
    action: "add_key",
    content: {
      hash: "exprv32bfqHX4VUoKei6SGQ19q53PHUdvZLnyadiFd4qvQwh2QRE47",
      key: {
        nat: "0",
        address: "tz1gKYy8uwdBHp9iw1PNiH7AJmzsvcVtmpwR",
      },
      value: "1",
    },
  },
];

```

### Errors

`N/not-minter - sender` of the transaction is not minter.

`N/wrong-collection-id -` In this method, this error means that there is no collection to minting.
