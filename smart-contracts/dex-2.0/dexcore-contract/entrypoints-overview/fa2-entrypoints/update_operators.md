# update\_operators

An entrypoint works exactly like FA2 _**update\_operators**_ entrypoint according to [TZIP-012](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md).

### Call parameters

```pascaligo
type token_id_t         is nat

type operator_t         is [@layout:comb] record [
  owner                   : address;
  operator                : address;
  token_id                : token_id_t;
]

type update_operator_t  is
| Add_operator            of operator_t
| Remove_operator         of operator_t

type update_operators_t is list(update_operator_t)
```

| Field     | Type         | Description        |
| --------- | ------------ | ------------------ |
| owner     | address      | Owner of tokens    |
| operator  | address      | Operator of tokens |
| token\_id | token\_id\_t | Token ID           |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = [
    {
        add_operator: {
            owner: "tz1.../KT1...",
            operator: "tz1.../KT1...",
            token_id: 0,
        },
    },
    {
        remove_operator: {
            owner: "tz1.../KT1...",
            operator: "tz1.../KT1...",
            token_id: 1,
         },
     },
     ...
];
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methods.update_operators(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `FA2_TOKEN_UNDEFINED` - token with `token_id` doesn't exist.
* `FA2_NOT_OWNER` - `sender` is not `owner` of account.
