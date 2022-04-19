# place\_bid

An entrypoint that allows anyone to place a bid in one of the active auctions.

{% hint style="warning" %}
You need to add the [Auction](../../) contract as the operator for your QUIPU tokens to make a bet.
{% endhint %}

### Call parameters

```pascaligo
type place_bid_t        is [@layout:comb] record [
  auction_id              : nat;
  bid                     : nat;
]
```

| Field       | Type | Description                   |
| ----------- | ---- | ----------------------------- |
| auction\_id | nat  | Auction's ID                  |
| bid         | nat  | A new bet on auctions' tokens |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const auctionAddress = "KT1...";
const params = 
    auction_id: 1,
    bid: 15,
};
const auction = await tezos.contract.at(auctionAddress);
const operation = await dexCore.methodsObject.place_bid(params).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `304` - auction with the specified ID not found.
* `308` - user's bid is less than minimum bid for an auction launch or less that previous bid.
* `309` - auction is already finished or rewards are already claimed.
* `311` - sender of a transaction isn't an account address (not `tz` address).
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
* `FA2_NOT_OPERATOR` - [Auction](../../) contract is not an `operator` for users' QUIPU tokens.
