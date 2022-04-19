# set\_flash\_swaps\_proxy

An entrypoint that setups a new **FlashSwapsProxy** contract for executing users' lambdas in time of flash swaps (see [FlashSwapsProxy](../../../flashswapsproxy-contract/)).

### Call parameters

| Field               | Type    | Description                                      |
| ------------------- | ------- | ------------------------------------------------ |
| flash\_swaps\_proxy | address | An address of a new **FlashSwapsProxy** contract |

### Usage

{% tabs %}
{% tab title="🌮 Taquito" %}
```javascript
const dexCoreAddress = "KT1...";
const flashSwapsProxyAddress = "KT1...";
const dexCore = await tezos.contract.at(dexCoreAddress);
const operation = await dexCore.methods.set_flash_swaps_proxy(flashSwapsProxyAddress).send();

await operation.confirmation();
```
{% endtab %}
{% endtabs %}

### Errors

* `400` - `sender` of the transaction is not current administrator.
* `412` - non payable entrypoint (can't accept TEZ tokens during call of an entrypoint).
