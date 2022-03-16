# 🛠 Developer module

This module contains storage with developer address, developer fee rate and its compiled setter lambdas.

### Module contents

#### Storage

Inside [standalone-dex](../standalone-dex/ "mention") and [factory](../factory/ "mention") contracts, storage contains the following structure:

```pascaligo
type main_storage_t   is [@layout:comb] record[
  //...
  dev_store             : dev_storage_t;
  //...
]

type storage_root     is [@layout:comb] record[
  //...
  storage               : main_storage_t;
  //...
]
```

This module expects the following structure and operates with the `dev_store` field. More details about module storage types are in section.

{% content-ref url="storage-and-action-types.md" %}
[storage-and-action-types.md](storage-and-action-types.md)
{% endcontent-ref %}

#### Setters

{% hint style="warning" %}
This entrypoints should be called only by `developer` address.&#x20;
{% endhint %}

All module fields have own setters. For calling this setters, used `call_dev` method.

{% code title="dev/methods.ligo" %}
```pascaligo
[@inline] function unwrap(
  const param           : option(_a);
  const error           : string)
                        : _a is
  case param of
  | Some(instance) -> instance
  | None -> failwith(error)
  end;

(* This methods called only by dev and modifies only `dev_storage` *)
[@inline] function call_dev(
  const p               : dev_action_t;
  var s                 : dev_storage_t)
                        : dev_storage_t is
  block {

    require(Tezos.sender = s.dev_address, Errors.not_developer);

    const idx : nat = case p of
    | Set_dev_address(_)  -> 0n
    | Set_dev_fee(_)      -> 1n
    end;

    const lambda_bytes : bytes = unwrap(s.dev_lambdas[idx], Errors.unknown_func);
    const func: dev_func_t = unwrap((Bytes.unpack(lambda_bytes) : option(dev_func_t)), Errors.wrong_use_function);
  } with func(p, s)
```
{% endcode %}

{% content-ref url="developer-setter-entrypoints/" %}
[developer-setter-entrypoints](developer-setter-entrypoints/)
{% endcontent-ref %}
