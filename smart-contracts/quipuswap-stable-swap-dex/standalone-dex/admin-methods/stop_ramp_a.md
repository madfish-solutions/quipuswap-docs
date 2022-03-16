# stop\_ramp\_A

{% hint style="warning" %}
This entrypoint should be called only by `admin` address.
{% endhint %}

This entrypoint is designed to stop ramping the "A" constant, when ramping in progress.

The new value of "A" fixed at time when stop is called.&#x20;

Call param type is `nat` - pool identifier.

### How to set `A` constant?

`A` constant set to contract in precalculated invariant value as

$$A_{storage} = A * n^{n-1}$$

so, if you want to set `A` correctly you should keep it in mind.
