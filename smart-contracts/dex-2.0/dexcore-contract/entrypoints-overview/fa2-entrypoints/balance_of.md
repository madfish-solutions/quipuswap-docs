# balance\_of

An entrypoint that retrieves a user's LP tokens amount and sends it to the callback contract. Works exactly like FA2 **balance\_of** entrypoint according to [TZIP-012](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md).

### Call parameters

```pascaligo
type token_id_t         is nat

type balance_request_t  is [@layout:comb] record [
  owner                   : address;
  token_id                : token_id_t;
]

type balance_response_t is [@layout:comb] record [
  request                 : balance_request_t;
  balance                 : nat;
]

type balance_of_t       is [@layout:comb] record [
  requests                : list(balance_request_t);
  callback                : contract(list(balance_response_t));
]
```

#### bal\_request\_t

| Field      | Type         | Description     |
| ---------- | ------------ | --------------- |
| owner      | address      | Owner of tokens |
| toeken\_id | token\_id\_t | Token ID        |

#### bal\_response\_t

| Field    | Type                                                 | Description        |
| -------- | ---------------------------------------------------- | ------------------ |
| requests | [bal\_request\_t](balance\_of.md#bal\_request\_type) | Balance of request |
| balance  | nat                                                  | Balance of token   |

#### balance\_of\_t

| Field    | Type                                                                   | Description         |
| -------- | ---------------------------------------------------------------------- | ------------------- |
| requests | list([bal\_response\_t](balance\_of.md#bal\_response\_type))           | Balance of requests |
| callback | contract(list([bal\_response\_t](balance\_of.md#bal\_response\_type))) | Callback contract   |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = [
    {
        owner: "tz1.../KT1...",
        token_id: 1,
    },
    ...
];
const dexCore = await tezos.contract.at(dexCoreAddress);
const result = await dexCore.contract.views
  .balance_of(params)
  .read();
```
{% endtab %}
{% endtabs %}

### Errors

* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
* `FA2_TOKEN_UNDEFINED` - token with `token_id` doesn't exist.
