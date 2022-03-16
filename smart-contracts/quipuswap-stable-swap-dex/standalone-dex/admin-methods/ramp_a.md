# ramp\_A

{% hint style="warning" %}
This entrypoint should be called only by `admin` address.
{% endhint %}

This entrypoint is designed to ramping the "A" constant, allowing to change "flattiness" of swap function.&#x20;

### How to set `A` constant?

`A` constant set to contract in precalculated invariant value as

$$A_{storage} = A * n^{n-1}$$

so, if you want to set `A` correctly you should keep it in mind.

### Call params

```pascaligo
type ramp_a_param_t     is [@layout:comb] record [
  pool_id                 : nat; 
  (* pool identifier *)
  future_A                : nat;
  (* target value of "A" constant *)
  future_time             : timestamp; 
  (* time when constant "A" would be reached target value *)
]
```
