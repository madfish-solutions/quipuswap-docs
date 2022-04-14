# claim

An entrypoint that allows the last person who made a bet to claim their tokens (only if auction is finished). The last bid is burned.

Burning means that all QUIPU tokens are transferred to the `zero_address`.

{% hint style="info" %}
`zero_address` is the account address that no one has access to: [`tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg`](https://tzkt.io/tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg/operations/)``
{% endhint %}

### Call parameters

```pascaligo
type claim_t            is nat // auction's ID
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const auctionAddress = "KT1...";
const auctionId = 5;
const auction = await tezos.contract.at(auctionAddress);
const operation = await dexCore.methods.claim(auctionId).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `304` - auction with the specified ID not found.
* `309` - auction is already finished or rewards are already claimed.
* `310` - auction is not finished.
