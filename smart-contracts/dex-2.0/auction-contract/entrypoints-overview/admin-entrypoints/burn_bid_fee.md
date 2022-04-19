# burn\_bid\_fee

An entrypoint that burns fee in [QuipuSwap Governance tokens](https://tzkt.io/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/operations/) which was deducted from users' bids.

Burning means that all QUIPU tokens are transferred to the `zero_address`.

{% hint style="info" %}
`zero_address` is the account address that no one has access to: [`tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg`](https://tzkt.io/tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg/operations/)``
{% endhint %}

### Call parameters

```pascaligo
type burn_bid_fee_t     is unit
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const auctionAddress = "KT1...";
const auction = await tezos.contract.at(auctionAddress);
const operation = await auction.methods.burn_bid_fee([]).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
