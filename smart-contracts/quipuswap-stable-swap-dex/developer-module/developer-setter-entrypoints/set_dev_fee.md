# set\_dev\_fee

Sets developer fee rate. Input value is `nat`.

{% hint style="info" %}
Fee stored as float value multiplied by `fee_denominator` = $$10^{10}$$
{% endhint %}

```pascaligo
function set_dev_fee(
  const p               : dev_action_t;
  var s                 : dev_storage_t)
                        : dev_storage_t is
  block {
    case p of
    | Set_dev_fee(fee) -> {
      require(fee < Constants.fee_denominator / 2n, Errors.Dex.fee_overflow);
      s.dev_fee := fee;
    }
    | _ -> skip
    end;
  } with s
```

<details>

<summary>Lambda bytes</summary>

050200000074037a072e02000000020320020000006407430368010000000c6665652d6f766572666c6f7707430362000207430362008090dfc04a0322072f020000001307430368010000000844495620627920300327020000000003160521000303190337072c020000000203200200000002032705500003

</details>
