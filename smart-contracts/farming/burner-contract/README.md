# Burner contract

Contract for receiving of TEZ tokens and burning them. After receiving of TEZ tokens it makes the exchange on [QuipuSwap DEX](https://quipuswap.com/swap/tez-KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb\_0) for QUIPU tokens and burns all of them.

Burning means that all exchanged QUIPU tokens are transferred to the `zero_address`.

{% hint style="info" %}
`zero_address` is the account address that no one has access to: [`tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg`](https://tzkt.io/tz1ZZZZZZZZZZZZZZZZZZZZZZZZZZZZNkiRg/operations/)``
{% endhint %}
