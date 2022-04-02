# Update\_operators

This method is used to **Add** or **Remove** balance operator. Operator is a Tezos address that originates token transfer operation on behalf of the owner.

### Call parameters

| Name                        | Type                                                                         | Description                   |
| --------------------------- | ---------------------------------------------------------------------------- | ----------------------------- |
| update\_operator\_params\_t | list([update\_operator\_param\_t](copy-of-copy-of-add\_minter.md#undefined)) | List of update operator param |

![](<../../../../../.gitbook/assets/image (12).png>)

| Field     | Type    | Description                                                                    |
| --------- | ------- | ------------------------------------------------------------------------------ |
| owner     | address | The address of the owner of the account to which the operator is being updated |
| operator  | address | New operator address                                                           |
| token\_id | nat     | Token ID                                                                       |

### Usage Add\_operator

{% code title="🌮 Taquito" %}
```javascript
const nftAddress = "KT1...";
const owner = "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc";
const operator = "tz1gKYy8uwdBHp9iw1PNiH7AJmzsvcVtmpwR"
const nftContract = await tezos.contract.at(nftAddress);
const operation = await nftContract.methods.update_operators([
        {
          "add_operator": {
            owner: owner,
            operator: operator,
            token_id: token_id,
          },
        },
      ]).send();

await operation.confirmation();
```
{% endcode %}

### Post conditions Add operator

![](<../../../../../.gitbook/assets/image (10).png>)

```json
[
  {
    bigmap: 219665,
    path: "allowances",
    action: "add_key",
    content: {
      hash: "exprut9brcqmzR6Yd3G6FnE5CPMPsF5YUTa8YgmykaoPQDvRVqz8nF",
      key: {
        nat: "0",
        address: "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc",
      },
      value: ["tz1gKYy8uwdBHp9iw1PNiH7AJmzsvcVtmpwR"],
    },
  },
];

```

### Usage Remove\_operator

{% code title="🌮 Taquito" %}
```javascript
const nftAddress = "KT1...";
const owner = "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc";
const operator = "tz1gKYy8uwdBHp9iw1PNiH7AJmzsvcVtmpwR"
const nftContract = await tezos.contract.at(nftAddress);
const operation = await nftContract.methods.update_operators([
        {
          "remove_operator": {
            owner: owner,
            operator: operator,
            token_id: token_id,
          },
        },
      ]).send();

await operation.confirmation();
```
{% endcode %}

### Post conditions Remove operator

![](<../../../../../.gitbook/assets/image (11).png>)

```json
[
  {
    bigmap: 219665,
    path: "allowances",
    action: "update_key",
    content: {
      hash: "exprut9brcqmzR6Yd3G6FnE5CPMPsF5YUTa8YgmykaoPQDvRVqz8nF",
      key: {
        nat: "0",
        address: "tz1YZYyXbRuSDnHrYJhugF7KhUojq3rtCyFc",
      },
      value: [],
    },
  },
];
```

### Errors

`FA2_NOT_OPERATOR - sender` of the transaction is not allowanced operator

`FA2_TOKEN_UNDEFINED - collection` does not exist.
