# mint\_tokens

An entrypoint for creating a transaction for minting a new [QuipuSwap Governance tokens](https://tzkt.io/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/operations/). Call of this entrypoint just generates mint QUIPU tokens transaction and sends it to the **QUIPU token** contract.

### Call parameters

```pascaligo
type mint_gov_tok_type  is [@layout:comb] record [
  receiver              : address;
  amount                : nat;
]

type mint_gov_toks_type is list(mint_gov_tok_type)
```

| Field    | Type    | Description                                 |
| -------- | ------- | ------------------------------------------- |
| receiver | address | Receiver of minted tokens                   |
| amount   | nat     | Amount of tokens to be minted to a receiver |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const proxyMinterAddress = "KT1...";
const receiver = "tz1.../KT1...";
const amount = 100;
const mintParams = [
    { receiver, amount },
    ...
];
const proxyMinter = await tezos.contract.at(proxyMinterAddress);
const operation = await proxyMinter.methods.mint_tokens(mintParams).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `ProxyMinter/sender-is-not-a-minter` - `sender` of the transaction is not registered by an administrator minter.
