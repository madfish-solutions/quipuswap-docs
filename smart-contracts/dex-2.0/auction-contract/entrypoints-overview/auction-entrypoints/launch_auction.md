# launch\_auction

An entrypoint that allows anyone to launch an auction for any **NON** whitelisted token.

{% hint style="warning" %}
You need to add the [Auction](../../) contract as the operator for your QUIPU tokens to make a first bet.
{% endhint %}

### Call parameters

```pascaligo
type tez_t              is unit

type fa12_token_t       is address

type fa2_token_t        is [@layout:comb] record [
  token                   : address;
  id                      : nat;
]

type token_t            is
| Tez                     of tez_t
| Fa12                    of fa12_token_t
| Fa2                     of fa2_token_t

type launch_auction_t   is [@layout:comb] record [
  token                   : token_t;
  amt                     : nat;
  bid                     : nat;
]
```

| Field | Type     | Description                     |
| ----- | -------- | ------------------------------- |
| token | token\_t | FA1.2/FA2/TEZ token             |
| amt   | nat      | Number of tokens for an auction |
| bid   | nat      | First bet on auctions' tokens   |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const auctionAddress = "KT1...";
const params = {
    token: {
        token: "KT1...",
        id: 0,
    },
    amt: 100,
    bid: 10,
};
const auction = await tezos.contract.at(auctionAddress);
const operation = await dexCore.methodsObject.launch_auction(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `305` - token for auction is whitelisted. It is not possible to start an auction with whitelisted tokens.
* `307` - [Auction](../../) contract have insufficient balance of tokens for a new auction launch.
* `308` - user's bid is less than minimum bid for an auction launch or less that previous bid.
* `FA2_NOT_OPERATOR` - [Auction](../../) contract is not an `operator` for users' QUIPU tokens.
