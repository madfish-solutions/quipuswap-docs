# 🛑 Admin methods

{% hint style="warning" %}
These entrypoints should be called only by `admin` address.
{% endhint %}

Section is about administrative management. Admin could change managers, self, update fee rates and manage "A" constant (manipulate flattness of swap function).

### Change admin address

Method allows admin to hand over its rights to another address.

{% content-ref url="set_admin.md" %}
[set\_admin.md](set\_admin.md)
{% endcontent-ref %}

### Update contract fee rates

Entrypoint designed to update all fee rates except developer fee.

{% content-ref url="set_fees.md" %}
[set\_fees.md](set\_fees.md)
{% endcontent-ref %}

### Add or remove token metadata managers

Method for add/remove manager addresses to manage LP token metadata.

{% content-ref url="add_rem_managers.md" %}
[add\_rem\_managers.md](add\_rem\_managers.md)
{% endcontent-ref %}

### Manipulate DEX pool "A" constant

Method to set new "A" constant. Changing performed distributed over time from old "A" to new "A".

{% content-ref url="ramp_a.md" %}
[ramp\_a.md](ramp\_a.md)
{% endcontent-ref %}

Method to stop changing "A" constant. The new "A" after stop would be specific "A" that counted at time of stopping (from ramping).

{% content-ref url="stop_ramp_a.md" %}
[stop\_ramp\_a.md](stop\_ramp\_a.md)
{% endcontent-ref %}
