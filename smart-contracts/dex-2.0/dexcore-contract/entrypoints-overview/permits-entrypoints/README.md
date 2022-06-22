# Permits' entrypoints

This section describes a permits part of a project. This part fully support [TZIP-017](https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-17/tzip-17.md).

### &#x20;Risks

Before you use a permit system we want to be sure you understand the following

1. Permits may not be timely submitted. Since the counter is a global variable, the counter may be increased already at the time the permit is submitted another one is processed by the permit entrypoint.
2. Existing permits may be guessed and executed.

{% content-ref url="permit.md" %}
[permit.md](permit.md)
{% endcontent-ref %}

{% content-ref url="set_expiry.md" %}
[set\_expiry.md](set\_expiry.md)
{% endcontent-ref %}
