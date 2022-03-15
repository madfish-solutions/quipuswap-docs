# Exceptions

In some cases, the contract's execution might fail. The current chapter describes the list of possible in-contract failures.

| Error                    | Description                                                                                                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| Dex/reentrancy           | It is prohibited to call the exchange until the previous operation is finished.                                     |
| Dex/function-not-set     | The code for the entrypoint doesn't exist in the bigmap. Should be unreachable.                                     |
| Dex/not-entered          | The contract can't be called until the previous method execution isn't finished.                                    |
| Dex/not-self             | The method should be called by the exchange contract only.                                                          |
| Dex/not-token            | The token doesn't implement the standard entrypoint.                                                                |
| Dex/not-close-entrypoint | The exchange contract doesn't have close entrypoint. Should be unreachable.                                         |
| Dex/not-launched         | The exchange for the pair isn't launched.                                                                           |
| Dex/no-liquidity         | Action can't be performed if there is no liquidity in the pool.                                                     |
| Dex/no-token-a-in        | The amount of invested token A can't be zero.                                                                       |
| Dex/no-token-b-in        | The amount of invested token B can't be zero.                                                                       |
| Dex/pair-exist           | The exchange can't be launched if it already exists.                                                                |
| Dex/wrong-route          | The exchange route isn't cohesive.                                                                                  |
| Dex/zero-amount-in       | Invest of zero tokens on one of the sides is not allowed.                                                           |
| Dex/insufficient-shares  | Not enough shares to burn.                                                                                          |
| Dex/dust-output          | One or all divested token amounts are zero.                                                                         |
| Dex/high-min-out         | The expected output is higher than the possible.                                                                    |
| Dex/wrong-pair-order     | The tokens should be provided in ascending order.                                                                   |
| Dex/empty-route          | The provided exchange route is empty.                                                                               |
| Dex/low-max-token-a-in   | The max amount of token A to deposit for the shares is insufficient.                                                |
| Dex/low-max-token-b-in   | The amount of token B to withdraw for the shares is too low.                                                        |
| Dex/action-outdated      | The operation isn't outdated.                                                                                       |
| Dex/wrong-reserves-state | After divest, some reserves and total shares aren't all zero or aren't all non-zero values. Should be unreachable.  |
| Dex/low-supply           | The amount of divested shares is higher than the total supply. Should be unreachable.                               |

