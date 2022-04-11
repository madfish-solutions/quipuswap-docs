# balance\_of

An entrypoint that retrieves a user's staked tokens amount and sends it to the callback contract. Works exactly like FA2 **balance\_of** entrypoint according to [TZIP-012](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md).

### Call parameters

```pascaligo
type token_id_type      is nat

type bal_request_type   is [@layout:comb] record [
  owner                   : address;
  token_id                : token_id_type;
]

type bal_response_type  is [@layout:comb] record [
  request                 : bal_request_type;
  balance                 : nat;
]

type balance_of_type    is [@layout:comb] record [
  requests                : list(bal_request_type);
  callback                : contract(list(bal_response_type));
]
```

#### bal\_request\_type

| Field      | Type            | Description     |
| ---------- | --------------- | --------------- |
| owner      | address         | Owner of tokens |
| toeken\_id | token\_id\_type | Token ID        |

#### bal\_response\_type

| Field    | Type                                                    | Description        |
| -------- | ------------------------------------------------------- | ------------------ |
| requests | [bal\_request\_type](balance\_of.md#bal\_request\_type) | Balance of request |
| balance  | nat                                                     | Balance of token   |

#### balance\_of\_type

| Field    | Type                                                                      | Description         |
| -------- | ------------------------------------------------------------------------- | ------------------- |
| requests | list([bal\_response\_type](balance\_of.md#bal\_response\_type))           | Balance of requests |
| callback | contract(list([bal\_response\_type](balance\_of.md#bal\_response\_type))) | Callback contract   |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const tFarmAddress = "KT1...";
const params = [
    {
        owner: "tz1.../KT1...",
        token_id: 1,
    },
    ...
];
const tFarm = await tezos.contract.at(tFarmAddress);
const result = await tFarm.contract.views
  .balance_of(params)
  .read();
```
{% endtab %}
{% endtabs %}

### Errors

An entrypoint doesn't throw any error.
