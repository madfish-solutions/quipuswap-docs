# transfer

An entrypoint that transfer user's LP tokens to another account (tz/KT). Also it votes for sender's and recipient's bakers. If the recipient does not have a preferred baker, the current delegated will be chosen as the preferred baker. Works exactly like FA2 transfer entrypoint according to [TZIP-012](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md). Also supports [TZIP-017](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-17/tzip-17.md) (permits).

### Call parameters

```pascaligo
type token_id_t         is nat

type transfer_dst_t     is [@layout:comb] record [
  to_                     : address;
  token_id                : token_id_t;
  amount                  : nat;
]

type transfer_t         is [@layout:comb] record [
  from_                   : address;
  txs                     : list(transfer_dst_t);
]

type transfers_t        is list(transfer_t)
```

#### transfer\_dst\_t

| Field     | Type         | Description                  |
| --------- | ------------ | ---------------------------- |
| to\_      | address      | Recipient of tokens          |
| token\_id | token\_id\_t | Token ID                     |
| amount    | nat          | Number of tokens to transfer |

#### transfer\_t

| Field  | Type                                                   | Description           |
| ------ | ------------------------------------------------------ | --------------------- |
| from\_ | address                                                | Sender of tokens      |
| txs    | list([transfer\_dst\_t](transfer.md#transfer\_dst\_t)) | Transfer transactions |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const params = [
    {
        from_: "tz1.../KT1...",
        txs: [
            {
                to_: "tz1.../KT1...",
                token_id: 1,
                amount: 100,
            },
            ...
        ],
    },
    ...
];
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methods.transfer(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `136` - reentrancy.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
* `FA2_TOKEN_UNDEFINED` - token with `token_id` doesn't exist.
* `FA2_NOT_OPERATOR` - `sender` is not `operator` of `from_` account or permit for transfer doesn't exist.
* `FA2_INSUFFICIENT_BALANCE` - transfer `amount` is greater than account `from_` balance.
* `EXPIRED_PERMIT` - someone is trying to transfer tokens using expired permit.
