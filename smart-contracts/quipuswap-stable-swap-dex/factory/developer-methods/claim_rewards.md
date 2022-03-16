# claim\_rewards

{% hint style="warning" %}
This contract method is called only by `developer` of that contract.
{% endhint %}

This entrypoint is very simple: it receives `unit` and withdraws all [QUIPU](https://better-call.dev/mainnet/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/metadata) tokens, collected as deployment fee.

```pascaligo
function claim_quipu(
  var s                 : full_storage_t)
                        : fact_return_t is
  block{
    const operations = list[
      typed_transfer(
        Tezos.self_address,              // Factory address (from)
        s.storage.dev_store.dev_address, // developer address (to)
        s.storage.quipu_rewards,         // amount of tokens
        Fa2(s.storage.quipu_token)       // FA2 QUIPU token
      )
    ];
    s.storage.quipu_rewards := 0n;
  } with (operations, s)
```
