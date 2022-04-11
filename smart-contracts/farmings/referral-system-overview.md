# Referral system overview

QuipuSwap Farmings implements referral system.

Every user can have only one referrer. In the beginning, users don't have referrers. A referrer can be changed by the user every his deposit (stake). Users can't refer themselves (transaction will fail in this case).

Every time when _**claim\_rewards**_ function is called (in _**deposit**_, _**withdraw**_, and _**harvest**_ entrypoints) _**harvest\_fee**_ will be minted/transferred to the user's referrer. If a user doesn't have a referrer, a _**harvest\_fee**_ will be minted/transferred to the `zero_address`.

{% hint style="info" %}
`zero_address` is the account address that no one has access to: [`tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg`](https://tzkt.io/tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg/operations/)``
{% endhint %}
