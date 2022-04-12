# update\_operators

An entrypoint works exactly like FA2 _**update\_operators**_ entrypoint according to [TZIP-012](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md).

### Call parameters

```pascaligo
type token_id_type      is nat

type operator_type      is [@layout:comb] record [
  owner         : address;
  operator      : address;
  token_id      : token_id_type;
]

type upd_operator_type  is
| Add_operator            of operator_type
| Remove_operator         of operator_type

type update_ops_type    is list(upd_operator_type)
```

| Field     | Type            | Description        |
| --------- | --------------- | ------------------ |
| owner     | address         | Owner of tokens    |
| operator  | address         | Operator of tokens |
| token\_id | token\_id\_type | Token ID           |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const tFarmAddress = "KT1...";
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
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methods.update_operators(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `FA2_NOT_OWNER` - `sender` is not `owner` of account.
