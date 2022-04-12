# transfer

An entrypoint that transfer user's staked tokens to another account (tz/KT). Also updates the rewards for these users. Votes for sender's and recipient's bakers if the farm supports TOK/TEZ QuipuSwap V1 LP tokens. If the recipient does not have a preferred baker, the current delegated will be chosen as the preferred baker. Works exactly like FA2 transfer entrypoint according to [TZIP-012](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md).

### Call parameters

```pascaligo
type token_id_type      is nat

type transfer_dst_type  is [@layout:comb] record [
  to_                     : address;
  token_id                : token_id_type;
  amount                  : nat;
]

type fa2_send_type      is [@layout:comb] record [
  from_                   : address;
  txs                     : list(transfer_dst_type);
]

transfer_type           of list(fa2_send_type)
```

#### transfer\_dst\_type

| Field     | Type            | Description                  |
| --------- | --------------- | ---------------------------- |
| to\_      | address         | Recipient of tokens          |
| token\_id | token\_id\_type | Token ID                     |
| amount    | nat             | Number of tokens to transfer |

#### fa2\_send\_type

| Field  | Type                                               | Description           |
| ------ | -------------------------------------------------- | --------------------- |
| from\_ | address                                            | Sender of tokens      |
| txs    | list([transfer\_dst\_type](transfer.md#undefined)) | Transfer transactions |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const tFarmAddress = "KT1...";
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
const tFarm = await tezos.contract.at(tFarmAddress);
const operation = await tFarm.methods.transfer(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `QSystem/farm-not-set` - farming with `fid` parameter doesn't exist.
* `ILLEGAL_TRANSFER` - transfer from the contract to the same contract (`Tezos.self_address`).
* `FA2_NOT_OPERATOR` - `sender` is not `operator` of `from_` account.
* `FA2_INSUFFICIENT_BALANCE` - transfer `amount` is greater than account `from_` balance.
* `TIMELOCK_NOT_FINISHED` - timelock of `sender` is not finished (only for farms with timelock).
