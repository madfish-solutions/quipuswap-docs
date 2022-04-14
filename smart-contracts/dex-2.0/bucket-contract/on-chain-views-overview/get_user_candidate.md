# get\_user\_candidate

This on-chain view returns current candidate of a user in voting. If a user didn't vote before, contract's current delegated baker will be returned.

### Call parameters

| Field | Type    | Description                                                        |
| ----- | ------- | ------------------------------------------------------------------ |
| user  | address | The user by which you want to find out the candidate in the voting |

### Return type

```pascaligo
key_hash
```

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const bucketAddress = "KT1...";
const user = "tz1.../KT1...";
const viewCaller = "tz1...";
const bucket = await tezos.contract.at(bucketAddress);
const candidate = await bucket.contract.contractViews.get_user_candidate(user).executeView({ viewCaller: viewCaller });
```
{% endtab %}
{% endtabs %}

### Errors

A view doesn't throw any errors.
