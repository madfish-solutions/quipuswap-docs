# ramp\_A

{% hint style="warning" %}
This entrypoint should be called only by `admin` address.
{% endhint %}

This entrypoint is designed to ramping the "A" constant, allowing to change "flattiness" of swap function.&#x20;

### How to set `A` constant?

`A` constant set to contract in precalculated invariant value as

$$A_{storage} = A * n^{n-1}$$

so, if you want to set `A` correctly you should keep it in mind.

### Call parameters

| Field        |     Type    | Description                                |
| ------------ | :---------: | ------------------------------------------ |
| pool\_id     | `pool_id_t` | pool identifier.                           |
| future\_A    |    `nat`    | the target value of "A" constant.          |
| future\_time | `timestamp` | timestamp when ramping should be finished. |

```pascaligo
type ramp_a_param_t     is [@layout:comb] record [
  pool_id                 : nat; 
  future_A                : nat;
  future_time             : timestamp;
]
```
