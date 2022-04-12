# ban\_bakers

An entrypoint that bans or unbans baker on the specified period (in seconds). Can ban/unban a group of bakers in one transaction. To unban baker, period of banning must be equal to 0.

### Call parameters

```pascaligo
type ban_baker_type     is [@layout:comb] record [
  baker                   : key_hash;
  period                  : nat;
]

type ban_bakers_type    is list(ban_baker_type)
```

| Field  | Type      | Description                                                             |
| ------ | --------- | ----------------------------------------------------------------------- |
| baker  | key\_hash | A baker address to ban or unban                                         |
| period | nat       | Period during which baker will be banned (in seconds). 0 to unban baker |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const qFarmAddress = "KT1...";
const params = [
    {
        baker: "tz1...",
        period: 43200, // 24 hours
    }
];
const qFarm = await tezos.contract.at(qFarmAddress);
const operation = await qFarm.methods.ban_bakers(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `Not-admin` - `sender` of the transaction is not current administrator.
