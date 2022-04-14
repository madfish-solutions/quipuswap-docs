# ⁉ Errors overview

All errors in the project are represented as string codes. The main purpose of this decision is the reduction of gas to be paid by users. Here you can find all errors codes and their explanation.

### DexCore errors

* `100` - unknown lambda function ID.
* `101` - lambda function is already set.
* `102` - wrong lambda function index (too high).
* `103` - can't unpack lambda function.
* `104` - wrong order of a tokens from parameters.
* `105` - zero token A amount in.
* `106` - zero token B amount in.
* `107` - pair (pool) with the specified `token_id` already listed.
* `108` - pair (pool) with the specified `token_id` not listed.
* `109` - pair doesn't have a liquidity.
* `110` - zero amount of LP tokens (shares) expected.
* `111` - low token A amount in.
* `112` - low token B amount in.
* `113` - a [Bucket](bucket-contract/) contract not found (not TOK/TEZ LP pair).
* `114` - insufficient liquidity.
* `115` - dust output (zero tokens amount expected).
* `116` - high expectations of output tokens.
* `117` - empty route of swaps.
* `118` - zero amount in was passed as the parameter.
* `119` - wrong route of a swap.
* `120` - wrong TEZ amount were passed to the transaction.
* `121` - [_**pour\_out**_](bucket-contract/entrypoints-overview/pour\_out.md) entrypoint of [Bucket](bucket-contract/) contract isn't found.
* `122` - [_**pour\_over**_](bucket-contract/entrypoints-overview/pour\_over.md) entrypoint of [Bucket](bucket-contract/) contract isn't found.
* `123` - [_**ban\_baker**_](bucket-contract/entrypoints-overview/ban\_baker.md) entrypoint of [Bucket](bucket-contract/) contract isn't found.
* `124` - [_**vote**_](bucket-contract/entrypoints-overview/vote.md) entrypoint of [Bucket](bucket-contract/) contract isn't found.
* `125` - [_**is\_banned\_baker**_](bucket-contract/on-chain-views-overview/is\_banned\_baker.md) view of [Bucket](bucket-contract/) contract isn't found.
* `126` - [_**default**_](flashswapsproxy-contract/entrypoints-overview/default.md) entrypoint of [FlashSwapsProxy](flashswapsproxy-contract/) contract isn't found.
* `127` - [_**get\_tez\_balance**_](bucket-contract/on-chain-views-overview/get\_tez\_balance.md) view of [Bucket](bucket-contract/) contract isn't found.
* `128` - [_**flash\_swap\_callback**_](dexcore-contract/entrypoints-overview/callbacks/flash\_swap\_callback.md) entrypoint of [DexCore](dexcore-contract/) contract isn't found.
* `129` - wrong amount of flash swap returns.
* `130` - referring on yourself is forbidden.
* `131` - [_**withdraw\_rewards**_](bucket-contract/entrypoints-overview/withdraw\_rewards.md) entrypoint of [Bucket](bucket-contract/) contract isn't found.
* `132` - insufficient interface fee balance.
* `133` - [_**get\_user\_candidate**_](bucket-contract/on-chain-views-overview/get\_user\_candidate.md) view of [Bucket](bucket-contract/) contract isn't found.
* `134` - [_**launch\_callback**_](dexcore-contract/entrypoints-overview/callbacks/launch\_callback.md#launch\_callback\_t) entrypoint of [DexCore](dexcore-contract/) contract isn't found.
* `135` - [_**receive\_fee**_](auction-contract/entrypoints-overview/auction-entrypoints/receive\_fee.md) entrypoint of [Auction](auction-contract/) contract isn't found.
* `136` - reentrancy.
* `137` - [_**close**_](dexcore-contract/entrypoints-overview/callbacks/close.md) entrypoint of [DexCore](dexcore-contract/) contract isn't found.
* `138` - only entered (transaction must be not the first transaction in the chain of calls).
* `139` - too few swaps.
* `140` - can't perform voting because of zero LPs balance of the user.
* `141` - wrong amount of TEZ tokens were attached to transaction.
* `142` - wrong reserves state after execution of the operation.
* `143` - `pair_id` parameter not provided (in case of withdrawing TEZ tokens).
* `144` - action outdated (the time until which the transaction remained valid was passed).

### Bucket errors

* `200` - [_**validate**_](bakerregistry-contract/entrypoints-overview/validate.md) entrypoint of [BakerRegistry](bakerregistry-contract/) contract isn't found.
* `201` - [_**get\_total\_supply**_](dexcore-contract/on-chain-views-overview/get\_total\_supply.md) view of [DexCore](dexcore-contract/) contract isn't found.
* `202` - [_**get\_collecting\_period**_](dexcore-contract/on-chain-views-overview/get\_collecting\_period.md) view of [DexCore](dexcore-contract/) contract isn't found.

### Auction errors

* `300` - unknown lambda function ID.
* `301` - can't unpack lambda function.
* `302` - wrong lambda function index (too high).
* `303` - lambda function is already set.
* `304` - auction with the specified ID not found.
* `305` - token for auction is whitelisted. It is not possible to start an auction with whitelisted tokens.
* `306` - token for withdrawing is NOT whitelisted.
* `307` - [Auction](auction-contract/) contract have insufficient balance of tokens for a new auction launch.
* `308` - user's bid is less than minimum bid for an auction launch or less that previous bid.
* `309` - auction is already finished or rewards are already claimed.
* `310` - auction is not finished.

### Common errors

* `400` - `sender` of the transaction is not current administrator.
* `401` - `sender` of the transaction is not current pending administrator (not the address that was assigned by the current administrator to the shift).
* `402` - `sender` of the transaction is not a manager.
* `403` - `sender` of the transaction is not [DexCore](dexcore-contract/) contract.
* `404` - _**transfer**_ entrypoint of FA12 token isn't found.
* `405` - _**transfer**_ entrypoint of FA2 token isn't found.
* `406` - not a nat (not an unsigned integer).
* `407` - wrong token type.
* `408` - division by zero.
* `409` - TEZ tokens receiver contract not found (not user account or contract doesn't have a `default` entrypoint).
* `410` - [_**fill**_](bucket-contract/entrypoints-overview/fill.md) entrypoint of [Bucket](bucket-contract/) contract isn't found.
* `411` - `pending_admin` in the storage of a contract is `None` (admin didn't call _**set\_admin**_ entrypoint).
