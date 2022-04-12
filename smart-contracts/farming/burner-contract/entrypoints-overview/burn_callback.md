# burn\_callback

An entrypoint receives the balance response from the **QUIPU token** contract for the **Burner** contract and transfers all QUIPU tokens from **Burner** contract to the `zero_address` (locks token forever).

### Usage

Only [QuipuSwap Governance token](https://tzkt.io/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/operations/) can call this entrypoint.

### Errors

* `Burner/not-QS-GOV-token` - `sender` is not the [QuipuSwap Governance token](https://tzkt.io/KT193D4vozYnhGJQVtw7CoxxqphqUEEwK6Vb/operations/).
