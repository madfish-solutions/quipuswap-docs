# permit

An entrypoint that implements creating of transfer permits. It fully implements [TZIP-017](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-17/tzip-17.md).

### Call parameters

```pascaligo
type blake2b_hash_t     is bytes

type permit_signature_t is michelson_pair(signature, "", blake2b_hash_t, "permit_hash")

type permit_t           is key * permit_signature_t
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
async function getPermitParamsHash(tezos, contract, entrypoint, parameter) {
  const raw_packed = await tezos.rpc.packData({
    data: contract.parameterSchema.Encode(entrypoint, parameter),
    type: contract.parameterSchema.root.typeWithoutAnnotations(),
  });

  return blake.blake2bHex(hex2buf(raw_packed.packed), null, 32);
}

async function createPermitPayload(tezos, contract, entrypoint, params) {
  const signerKey = await tezos.signer.publicKey();
  const permitCounter = await contract.storage().then(storage => storage.storage.permits_counter);
  const paramHash = await getPermitParamsHash(tezos, contract, entrypoint, params);
  const chainId = await tezos.rpc.getChainId();
  const bytesToSign = await tezos.rpc.packData({
    data: permitSchema.Encode({
      0: contract.address,
      1: chainId,
      2: permitCounter,
      3: paramHash,
    }),
    type: permitSchemaType,
  });
  const signature = await tezos.signer.sign(bytesToSign.packed).then(s => s.prefixSig);

  return [signerKey, signature, paramHash];
}

const dexCoreAddress = "KT1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const transferParams = [
  {
    from_: alice.pkh,
    txs: [
      {
        to_: bob.pkh,
        token_id: 0,
        amount: 100,
      },
      ...
    ],
  },
  ...
];
const [signerKey, signature, permitHash] = await createPermitPayload(tezos, dexCore, "transfer", transferParams);
const operation = await dexCore.methods.permit(signerKey, signature, permitHash).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `DUP_PERMIT` - user is trying to create duplicate of an existing permit.
* `MISSIGNED` - incorrect signature of a permit.
