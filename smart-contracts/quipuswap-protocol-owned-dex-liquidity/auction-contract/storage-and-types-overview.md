# 💾 Storage and types overview

{% hint style="info" %}
Postfix `_f` means that the number is multiplied by a system precision.
{% endhint %}

### token\_t

![](<../../../.gitbook/assets/image (13).png>)

### Storage

![](<../../../.gitbook/assets/image (11).png>)

### storage\_t

| Field                | Type                                                                                                                                | Description                                                               |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| owner                | <mark style="color:red;">address</mark>                                                                                             | Contract owner                                                            |
| bid\_asset           | [token\_t](storage-and-types-overview.md#common-types)                                                                              | Bid asset, FA2 standard LP shares                                         |
| distributor\_address | <mark style="color:red;">address</mark>                                                                                             | The address of the NFT to be distributed as a lot for winning the auction |
| auction\_duration    | <mark style="color:green;">nat</mark>                                                                                               | Auction duration                                                          |
| initial\_bid         | <mark style="color:green;">nat</mark>                                                                                               | Initial bid                                                               |
| min\_bid\_step       | <mark style="color:green;">nat</mark>                                                                                               | Minimal bid step                                                          |
| bid\_fee\_rate_\__f  | <mark style="color:green;">nat</mark>                                                                                               | Percentage of commission from the bet                                     |
| auction\_count       | <mark style="color:green;">nat</mark>                                                                                               | Auctions counter                                                          |
| auctions             | <mark style="color:yellow;">big\_map</mark>_(nat,_ [auction\_t](storage-and-types-overview.md#ledger\_key\_t-is-tuple-address-nat)) | Mapping auction\_id to auction\_t                                         |
| fee\_balance         | <mark style="color:green;">nat</mark>                                                                                               | Balance of commissions collected                                          |
| auction\_enabled     | <mark style="color:blue;">bool</mark>                                                                                               |  auction status                                                           |
| metadata             | <mark style="color:yellow;">big\_map</mark>(string, bytes)                                                                          | Smart contract metadata                                                   |

### auction\_t

| Field           | Type                                         | Description                              |
| --------------- | -------------------------------------------- | ---------------------------------------- |
| end\_time       | <mark style="color:purple;">timestamp</mark> | Auction end time                         |
| current\_bid    | <mark style="color:green;">nat</mark>        | Current amount bid                       |
| current\_bidder | <mark style="color:red;">address</mark>      | The address of the one whose current bid |
| finished        | <mark style="color:blue;">bool</mark>        | Flag indicating that the auction is over |



###
