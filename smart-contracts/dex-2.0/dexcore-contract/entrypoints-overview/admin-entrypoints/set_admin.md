# set\_admin

Changing of the contract administrator is done in 2 steps:

1. Current administrator should transfer his rights to a new administrator.
2. A new administrator must accept his new role. If he didn't accept a new role, the previous administrator continues to be an administrator of this contract.

This entrypoint describes the first step of changing the contract administrator. The second step is described [here](confirm\_admin.md).

### Call parameters

| Field | Type    | Description                         |
| ----- | ------- | ----------------------------------- |
| admin | address | A new administrator of the contract |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const admin = "tz1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methods.set_admin(admin).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
