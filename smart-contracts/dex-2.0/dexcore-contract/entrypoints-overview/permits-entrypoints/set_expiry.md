# set\_expiry

An entrypoint that setups an expiry for a specific user's transfer permit or default expiry for all user's transfer permits. It fully implements [TZIP-017](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-17/tzip-17.md).

### Call parameters

```pascaligo
type seconds_t          is nat

type blake2b_hash_t     is bytes

type set_expiry_t       is [@layout:comb] record [
  issuer                  : address;
  expiry                  : seconds_t;
  permit_hash             : option(blake2b_hash_t);
]
```

| Field        | Type                     | Description                  |
| ------------ | ------------------------ | ---------------------------- |
| issuer       | address                  | An issuer of a permit        |
| expiry       | seconds\_t (nat)         | Expiry for a permit to setup |
| permit\_hash | option(blake2b\_hash\_t) | Hash of a permit (optional)  |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const hash = "...";
const params = {
    issuer: "tz1.../KT1...",
    expiry: 100, // in seconds
    permit_hash: hash, // or undefined, or null
};
const operation = await dexCore.methodsObject.set_expiry(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `NOT_PERMIT_ISSUER` - a user is not an issuer of the permit.
* `EXPIRY_TOO_BIG` - expiry from parameters is bigger than maximum available expiry (`31 556 995 200` seconds or `1000` years).
