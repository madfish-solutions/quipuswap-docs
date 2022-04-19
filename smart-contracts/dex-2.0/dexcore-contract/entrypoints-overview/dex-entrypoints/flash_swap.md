# flash\_swap

An entrypoint that allows to make a flash swaps. QuipuSwap flash swaps allow you to withdraw up to the full reserves of any FA1.2/FA2/TEZ token on QuipuSwap and execute arbitrary logic at no upfront cost, provided that by the end of the transaction you either:

* pay for the withdrawn FA1.2/FA2/TEZ tokens with the corresponding pair tokens;
* return the withdrawn FA1.2/FA2/TEZ tokens along with a small fee.

After execution of user's lambda, [_**flash\_swap\_callback**_](../callbacks/flash\_swap\_callback.md) entrypoint will be executed.

### Call parameters

```pascaligo
type token_id_t         is nat

type flash_swap_rule_t  is
| Loan_a_return_a
| Loan_a_return_b
| Loan_b_return_a
| Loan_b_return_b

type flash_swap_t       is [@layout:comb] record [
  lambda                  : unit -> list(operation);
  flash_swap_rule         : flash_swap_rule_t;
  pair_id                 : token_id_t;
  deadline                : timestamp;
  receiver                : address;
  referrer                : address;
  amount_out              : nat;
]
```

| Field             | Type                    | Description                                                                                                                    |
| ----------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| lambda            | unit -> list(operation) | Users's lambda function that doesn't accept any parameters (_**unit**_) and returns a list of operations (transactions, calls) |
| flash\_swap\_rule | flash\_swap\_rule\_t    | Rule of a flash swap (which token to take and which token to return)                                                           |
| pair\_id          | token\_id\_t (nat)      | Identifier of the liquidity pool (pair)                                                                                        |
| deadline          | timestamp               | The time until which the transaction remains valid and will not be rejected                                                    |
| receiver          | address                 | Receiver of taken tokens (most often a contract)                                                                               |
| referrer          | address                 | Referrer to whom interface fee will be paid                                                                                    |
| amount\_out       | nat                     | The number of outgoing tokens                                                                                                  |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
import { execSync } from "child_process";

const dexCoreAddress = "KT1...";
const params = {
    flash_swap_rule: "Loan_a_return_a",
    pair_id: 1,
    deadline: String(Date.parse((await tezos.rpc.getBlockHeader()).timestamp) / 1000 + 100),
    receiver: "KT1...", // a contract that will execute arbitrary logic or do smth with received tokens
    referrer: "tz1.../KT1...",
    amount_out: 1000,
};
const stdout = execSync(
    `${ligo} compile parameter ${lambda_file} 'Use(Flash_swap(record [ lambda = ${lambda_name}; flash_swap_rule = ${
      params.flash_swap_rule
    }; pair_id = ${params.pair_id.toString()}n; deadline = (${
      params.deadline
    } : timestamp); receiver = ("${
      params.receiver
    }" : address); referrer = ("${
      params.referrer
    }" : address); amount_out = ${params.amount_out.toString()}n ] ))' -p hangzhou --michelson-format json`,
    { maxBuffer: 1024 * 500 }
).toString();
const operation = await tezos.contract.transfer({
    to: dexCoreAddress,
    amount: 0,
    parameter: {
      entrypoint: "use",
      value: JSON.parse(stdout).args[0],
    },
    fee: 1000000,
    gasLimit: 1040000,
    storageLimit: 20000,
});

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Lambda function example

FlashSwapAgent - contract that implements different arbitrary logic.

```pascaligo
const agent : address = ("KT1LZjpR3hysVYyji1bfgNHJAuZhiQApUd71" : address);
const val : nat = 100n;

function get_flash_swap_agent_default_entrypoint(
  const agent           : address)
                        : contract(nat) is
  Tezos.get_contract_with_error(agent, "FlashSwapAgent/default-entrypoint-404")

function lambda(const _ : unit) : list(operation) is
  list [
    Tezos.transaction(
      val,
      0mutez,
      get_flash_swap_agent_default_entrypoint(agent)
    )
  ]
```

### Errors

* `108` - pair (pool) with the specified `token_id` not listed.
* `114` - insufficient liquidity.
* `115` - dust output (zero tokens amount expected).
* `130` - referring on yourself is forbidden.
* `136` - reentrancy.
* `144` - action outdated (the time until which the transaction remained valid was passed).
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
* all errors from the [_**flash\_swap\_callback**_](../callbacks/flash\_swap\_callback.md) entrypoint.
