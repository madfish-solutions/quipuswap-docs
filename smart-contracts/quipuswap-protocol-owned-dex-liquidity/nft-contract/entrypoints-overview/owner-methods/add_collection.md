# Add\_collection

This method is used to add new NFT collection.

### Call parameters&#x20;

![](<../../../../../.gitbook/assets/image (4).png>)

| Field       | Type               | Description                                                                                                                |
| ----------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| max\_supply | nat                | The maximum number of tokens that can be minted                                                                            |
| metadata    | map(string, bytes) | Metadata of the new collection  metadata conforming to [TZIP-21](https://tzip.tezosagora.org/proposal/tzip-21/) standards. |

### Usage

{% code title="🌮 Taquito" %}
```javascript
const { MichelsonMap } = require("@taquito/michelson-encoder");

const nftAddress = "KT1...";
const nftContract = await tezos.contract.at(nftAddress);
const tokenMeta = MichelsonMap.fromLiteral({
  decimals: Buffer.from("0").toString("hex"),
  isBooleanAmount: Buffer.from("0").toString("hex"),
  name: Buffer.from("NFT test").toString("hex"),
  symbol: Buffer.from("NTT").toString("hex"),
  description: Buffer.from("Test NTF collection").toString("hex"),
  minter: Buffer.from("tz1gKYy8uwdBHp9iw1PNiH7AJmzsvcVtmpwR").toString("hex"),
  creators: Buffer.from(JSON.stringify(["Madfish.Solutions"])).toString("hex"),
  date: Buffer.from("2021-11-19T00:00:00+00:00").toString("hex"),
  type: Buffer.from("Digital Nft").toString("hex"),
  tags: Buffer.from(JSON.stringify(["TestNFT", "collectibles"])).toString(
    "hex",
  ),
  language: Buffer.from("en").toString("hex"),
  artifactUri: Buffer.from(
    "https://hatrabbits.com/wp-content/uploads/2017/01/random.jpg",
  ).toString("hex"),
  displayUri: Buffer.from(
    "https://hatrabbits.com/wp-content/uploads/2017/01/random.jpg",
  ).toString("hex"),
  thumbnailUri: Buffer.from(
    "https://hatrabbits.com/wp-content/uploads/2017/01/random.jpg",
  ).toString("hex"),
  attributes: Buffer.from(
    JSON.stringify([
      {
        name: "Rarity",
        value: "Сommon",
      },
    ]),
  ).toString("hex"),
});

const operation = await nftContract.methods.add_collection(100, tokenMeta).send();

await operation.confirmation();
```
{% endcode %}

### Post conditions&#x20;

![](<../../../../../.gitbook/assets/image (9).png>)

### Errors

`N/not-owner - sender` of the transaction is not current owner.
