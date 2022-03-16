# set\_dev\_address

Sets new developer address. Input value is `address`.

```pascaligo
(* Sets dev address *)
function set_dev_address(
  const p               : dev_action_t;
  var s                 : dev_storage_t)
                        : dev_storage_t is
  case p of
  | Set_dev_address(new_dev) -> s with record [dev_address = new_dev]
  | _ -> s
  end
```

<details>

<summary>Lambda bytes</summary>

050200000014037a072e02000000040550000102000000020320

</details>
