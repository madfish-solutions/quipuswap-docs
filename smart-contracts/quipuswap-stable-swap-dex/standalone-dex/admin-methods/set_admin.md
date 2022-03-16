# set\_admin

{% hint style="warning" %}
This entrypoint should be called only by `admin` address.
{% endhint %}

This entrypoint is designed to change administrator address.&#x20;

Call param type is `address` - the new administator address.

```pascaligo
(* Sets admin of contract *)
function set_admin(
  const p               : admin_action_t;
  var s                 : storage_t)
                        : return_t is
  case p of
  | Set_admin(new_admin) -> (
     Constants.no_operations, 
     s with record [ admin = new_admin ]
  )
  | _ -> (Constants.no_operations, s)
  end
```
