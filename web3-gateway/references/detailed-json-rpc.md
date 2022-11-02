---
description: >-
  A detailed overview of supported Ethereum JSON RPC calls.
---

{% hint style='info'%}
This page shows detailed overview of supported Ethereum JSON RPC calls.
Find a [brief list of supported calls](detailed-json-rpc.md).
{% hint %}

## `eth_getBlockByHash`

Returns information about a block by hash.

[Brief version](detailed-json-rpc.md#eth_getBlockByHash)

**PARAMS**

1. **Block hash**The hash of the block `STRING` 32 byte hex value

1. **Hydrated transactions** `BOOLEAN` hydrated
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockByHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    false
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockByHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    false
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBlockByHash() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBlockByHash(
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    false
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBlockByHash();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "number": "0x77ed36",
    "hash": "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "parentHash": "0xdf9734476dcc360d864e31cc8422ce96f8aa8dff9a827b57f2c3c4ec8f71c421",
    "nonce": "0x0000000000000000",
    "mixHash": "0x3dd2d65fcd45d469cdca6e524382053d27b9e36b2b2e2f5808247c406d6bafd5",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "logsBloom": "0x00300000000000080000000800800800000040c000080012000888102002041000000000020002000020000040000800000008000002404100001000402468300844000080000008880800280808090000000001001400000000290040000800000400004200088001402280800008120d000040104000000000001000800080000000840060480001020000000005000000008028000204010208008020004002050800500002900000083080000000010000010400006100100000000000200804900200000800051400001800a050000008240001001000000028008060201034004000020011200008080000008880080008000048019040000081000010",
    "stateRoot": "0x1a6a2f5902392bf771ec405d427eae2df1c634ed26705e182e48adb893e2fa22",
    "miner": "0x4d496ccc28058b1d74b7a19541663e21154f9c84",
    "difficulty": "0x0",
    "extraData": "0x",
    "size": "0xead",
    "gasLimit": "0x1c9c380",
    "gasUsed": "0x20af8f",
    "timestamp": "0x635e2a44",
    "transactionsRoot": "0x24254b70d82f362e21f82ca841a893d1fe714fcdadba260fac0032359a40d9d8",
    "receiptsRoot": "0x956eb9e1ec572a6d044663dc0085bf421d6cf49193e383b4dc004c36e2f676e5",
    "baseFeePerGas": "0x10",
    "totalDifficulty": "0xa4a470",
    "uncles": [],
    "transactions": [
      "0xea5bbd6f391894557eec975d161391f25ce4cf86cc404964a2c39957b11dad43",
      "0x08f23a8d29dc0b23989b648f11fd89fad609c6694305b5d35e9b6d5fe1616d3a",
      "0x912b1146c5bc2c17b2e0726cc43d51ba9d22e19cd0a38dd248062520349db02b",
      "0xf10ba2f27477339095f9e7b60611812d6ca2a75e69e72f6acb64e2b109ae74b8",
      "0x559fd3851c1470cac199885335676fedcdde9789aee0ad894feef6705be7139c",
      "0x2ecf200a6c4da6478430acfac77a58fe90bd9c7db8c5bc19059eecd87dbb6794",
      "0xe5227c1cc37b2c7af8ef050fbc56913425b01b82b1866fa5099ba512630ae7d1",
      "0x4033bed32cca181377b703e742f092142447a0ab65ae4c1fb8a156d816ac397f",
      "0x6d8d45835f7101188cb9e7b5e8fb18e3d1fdc3bd26e3417ffbed63423a936c37",
      "0xe78704b2a82a49603ca2cdeffde7543911b68207ff397ed756e19da125e3eda6"
    ]
  }
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Block information
Block object `OBJECT`

- **parentHash** `STRING` Parent block hash
- **sha3Uncles** `STRING` Ommers hash
- **miner** `STRING` Coinbase
- **stateRoot** `STRING` State root
- **transactionsRoot** `STRING` Transactions root
- **receiptsRoot** `STRING` Receipts root
- **logsBloom** `STRING` Bloom filter
- **difficulty** (_optional_) `STRING` Difficulty
- **number** `STRING` Number
- **gasLimit** `STRING` Gas limit
- **gasUsed** `STRING` Gas used
- **timestamp** `STRING` Timestamp
- **extraData** `STRING` Extra data
- **mixHash** `STRING` Mix hash
- **nonce** `STRING` Nonce
- **totalDifficulty** (_optional_) `STRING` Total difficult
- **baseFeePerGas** (_optional_) `STRING` Base fee per gas
- **size** `STRING` Block size
- **transactions** `ANYOF` of

  - Transaction hashes `ARRAY` of `STRING` 32 byte hex value

  - Full transactions `ARRAY` of

    - Signed 1559 Transaction `OBJECT`

      - **type** `STRING` type
      - **nonce** `STRING` nonce
      - **to** (_optional_) `STRING` to address
      - **gas** `STRING` gas limit
      - **value** `STRING` value
      - **input** `STRING` input data
      - **maxPriorityFeePerGas** `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
      - **maxFeePerGas** `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
      - **accessList** accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
        - **address** (_optional_) `STRING` hex encoded address
        - **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
      - **chainId** `STRING` chainId: Chain ID that this transaction is valid on.
      - **yParity** `STRING` yParity: The parity (0 for even, 1 for odd) of the y-value of the secp256k1 signature.
      - **r** `STRING` r
      - **s** `STRING` s

    - Signed 2930 Transaction `OBJECT`

      - **type** `STRING` type
      - **nonce** `STRING` nonce
      - **to** (_optional_) `STRING` to address
      - **gas** `STRING` gas limit
      - **value** `STRING` value
      - **input** `STRING` input data
      - **gasPrice** `STRING` gas price: The gas price willing to be paid by the sender in wei
      - **accessList** accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
        - **address** (_optional_) `STRING` hex encoded address
        - **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
      - **chainId** `STRING` chainId: Chain ID that this transaction is valid on.
      - **yParity** `STRING` yParity: The parity (0 for even, 1 for odd) of the y-value of the secp256k1 signature.
      - **r** `STRING` r
      - **s** `STRING` s

    - Signed Legacy Transaction `OBJECT`
      - **type** `STRING` type
      - **nonce** `STRING` nonce
      - **to** (_optional_) `STRING` to address
      - **gas** `STRING` gas limit
      - **value** `STRING` value
      - **input** `STRING` input data
      - **gasPrice** `STRING` gas price: The gas price willing to be paid by the sender in wei
      - **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.
      - **v** `STRING` v
      - **r** `STRING` r
      - **s** `STRING` s

- **uncles** Uncles `ARRAY` of `STRING` 32 byte hex value

## `eth_getBlockByNumber`

Returns information about a block by number.

[Brief version](detailed-json-rpc.md#eth_getBlockByNumber)

**PARAMS**

1. **Block**

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

1. **Hydrated transactions** `BOOLEAN` hydrated
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockByNumber",
  "params": ["latest", false]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockByNumber",
  "params": [
    "latest",
    false
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBlockByNumber() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBlockByNumber("latest", false);

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBlockByNumber();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "number": "0x77f0f5",
    "hash": "0x127c828fda7de247574cd0da8e71a5aa77061399dcc32ae69ca6416b51d00b6d",
    "parentHash": "0xad2bd027835daad63b7e08619f957cfa37f61749d6fdca7d693cf0b302f7e5e7",
    "nonce": "0x0000000000000000",
    "mixHash": "0xe7ed0061aa3459a21d6a95ec47053bbe110d72bc0bc6d68757bbaeb4d626c5bc",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "logsBloom": "0x1efc0a11efad40dc9934f5de85d31ad5c2fead44f52d1b9fa08dbdbbfa977575078d0d69af1b3edea3d053b674e708ccd43bbae3115b4e65c516b74efdb47e73bb57d3a3d7f7888dbcefbabb5d6fa9263887ed5ba594ba61ffd6bbbcacbe29d61f00765152668be27e7964b0c9558cf6dc485201cf4d4b5fe006da9572d47058f87759ecdce4eda2c0debb25f1b6773e8024cda1e328c78e831f38fdf48263d8dff7cdf13bdbed129bcfb57a97f63592b3bc6bc1474fd5ed435c6c3b7328baf6ab7c5546fab9f4e1e7f0f545558af77c3a8d2f27f69f2439da755f2f4fe9efb8995dfdf0b6de77d39717c3de846167bec55b9d4e4ebbc5ddde5098bfb36302b9",
    "stateRoot": "0xeeb490efdb9c919746554bee78bae95657131e4865ac310b79dbe0a012d102ec",
    "miner": "0xc6e2459991bfe27cca6d86722f35da23a1e4cb97",
    "difficulty": "0x0",
    "extraData": "0x",
    "size": "0x20412",
    "gasLimit": "0x1c9c380",
    "gasUsed": "0x190246b",
    "timestamp": "0x635e6764",
    "transactionsRoot": "0x7f4e4e19406767174747db9016c8117cb794537de31a3891e94ea5914a6a99f9",
    "receiptsRoot": "0x103673c27ed4ca9963b929d7488866fa913115397faecd339b60676efc458b4c",
    "baseFeePerGas": "0x1025a28ca",
    "totalDifficulty": "0xa4a470",
    "uncles": [],
    "transactions": [
      "0x890099366f5a47200019fadbaf5bf7f1d31453e2460319dfc6c77d643edcd058",
      "0x502dd68d305c2d713a46003718c0d261bdc8a3d136fad71a955d3d3e1096dbb6",
      "0x44bd991e35a3a5d55c908bbdbca1392099d2b439ef8e48e6c352f4f814fefed6",
      "0x6fe41ac4698cc5e2a929a168afada126971917f37f8f6e51993047a0c6f30c28",
      "0xbe13c47eeb0307f90d93338b44a2f17cc51af53da90baab55f40dc19f78f643d",
      "0x137d01b87288c3f5a66e421a03a26c33da5f0b654d71f7ba436343d7836d5474",
      "0x4481fe28f32079664adb7563883a0d0ce8fdf25b027293bfe7925e61d31e1361",
      "0x6de72b99cd302a5906bb745132cf9ec1c226e22f051ef4db8631cb43c054145e",
      "0xe1ef5b7d6ae186f75f286ae16accb97575d1fda6763c42cb551f1a4466da58dd",
      "0x41f741ae989111e7bba590f6418af642f24d84505a4519da014b342a948ce276",
      "0xc57401f59adce6d6701f938bb2f7f6fdfb3b90b7772bd2a36573667cfec5a3a4",
      "0xae259c30216b4686a03294f0b422cd0a2457d876be367dd3b883a263f608324d",
      "0x8c1463b1223489aed43608c597ca0e47f55618df9b0c1ea6f58d9e88c2a6b580",
      "0xd195e2efd942b529b1a7e05071d917ef738b8b46272bf4ff07ff5ab9299381a2",
      "0x0328165aa0add7c31078b1305ce4149e107e52196445d87493be2252843eb303",
      "0x1eb57061ac583aacd57c83c625df497c41db02f73b22044a35c10dca2fd2c1c2",
      "0x9861c81221493ba2dc7944b05e62100fa70b0dfaee2c037b12ca6eb8aa73b90a",
      "0x438e63dbc04dbf75a21b861cee00f3251dd3a92b5093dcb33775952a748433b4",
      "0x318471211a49e98421c451e0369ae804865513e18b9e4c6a4f989a7bffb3e2ed",
      "0xf0434311c181f380c4a5898d885f16c23957432c0f4e17cc1af0440e6f4156f5",
      "0x5750cc0c61950adb667c27d96c019f3788b8a7f6c086e32c4509f6b97ddc42e0",
      "0xa8455f5937758ee59cbfacb767cd39a55de657ed1633c3f203386713c65178ab",
      "0x201dbe1cf25c9fd4763455844861829b7a8a7043c445416513a1280b111ab2ef",
      "0x73e43087d4f8f3ab5dc3b7850c1a90f4bfd64eeda400cd1868d126aeb35b96a8",
      "0xa771936055f2b9c86ac3f01682013199560d5cb0fb29b091eb1d027b790837d7",
      "0x8cb1a9807caa9c1122d905b89aad6af8d2367415c9ed09e9d35f2d94f776993b",
      "0x44e3f192ccf79a9250987dad1e825891b5f2a783ae14bba104cefa351b56b6b2",
      "0x89e0b8de2b51533ca8151c7ddd966a287493acd50bfb9a2f272c28bb725a8c6d",
      "0xe9b0cbfd257619f90a7b364a0809da72e70e797ec0ae5612c85551f6ab8fd66f",
      "0xf5d503b5f837128b71e81506ddc42687b3cb14d68b4fbd42cd1091238349b915",
      "0xdd6aa8c0a4403158571ebd10b32314319422b0f67d8ca13a9d36be579305cc52",
      "0x20a44cb47a01637549f03d2e9dea2088c22a42414e42019742f0c88303890d76",
      "0x605fb9821d5f2b97dd364597556eb726e4c9c7868b9e2b02b830526ecc881703",
      "0x60ce435cf099eaf8c63e51664af1697bfe24a8abd6b1c917eb05f889d3753f28",
      "0x5fa61c4942cd87b065f3085988026f4a5266d05a1140fb580294759c2d3bcb4b",
      "0x4fa2671177f382174fe65bf722f4d2eb0d5e5b50d9622fa6e1c2626ec22c5463",
      "0x2bbeca8b8d1e1201d2cec11d53a6b5eaefdebeb6d01da4b810144a6db6be3008",
      "0xf40479596bb2f0ee4f7cc6c474154fd69a91c3cd4e9448ab8f730590c853bf62",
      "0xaea8ba1523193f8bd57eb07d6ce5dfd9a41438a4c626e5bc4de2e5f62cca3e9d",
      "0xe8d08752fc2c5484f622db6f0a255e8b67e4c144275dbfa0511dcc74e6621ca1",
      "0x75c1ddb34801404960bd0bc615edf80f0881d9bd134867105bc92ccb4e1ed3ae",
      "0xa1d471b114cd622c77199bbe11d8f0a674ee5bd2c8051226c5e17ee8ecf995d6",
      "0x2494180988b6b4270396caa735ae5d584ca1a97ca6fa3cd6a877594a5f896e75",
      "0x59b1ee30bbc7cc313d488a5ee7cd936ed652225266031c1be7437e0b0778bfb0",
      "0xe6ff205a5f3737d3e788d4bcc85972a549276e0599f510aa721055e4f4478d75",
      "0xc440e118d777d77279a590ede5f94db62d53513accb57e9ebbd7d45ab304e565",
      "0xa06c8546b8366d957fd7dda779a420e28e25562676d2167a8f9714b294cd9f4f",
      "0x85d52967eadd25b19c2cde19c200d9e0d2be515205fa6dec874e572bdd625086",
      "0xda92a575d69016c30a64219509c95395317140d1311a12fd6bb17123a723f5af",
      "0x7f6b71e35b93281379b8e73e027072b51bd29e431a0704e66747ee496ed728e6",
      "0x5803d2fba48e2bf1bc7cbabba864c26f2e600553a9c78e364fe776bc21c766a3",
      "0x2d5f8e75328082a6705b44afd3a73e07d71bcf183d6cbbfed0f3234dd84d011d",
      "0x591756ab4cdc7a2ec2d346eb686c5467fd3c9f56bf86f3687c48528179d17c0a",
      "0x639e6f8f68154b313e0039235f5ce988da32b6f260f7282262d994a5b311a549",
      "0x910c389725487b5ec5cff003a15ac390ba893e8f85701cdaa2ca56a7e5377d00",
      "0x40afe02d0cffdbcbd41f7fde85e922378d474a646925a41a1473fcade8baf636",
      "0x112d4f811777a5801e1fd73aceea7cf51df61f7be5e413439135e89a02711320",
      "0xe7f949601bddfcfc9a582d01ac29fda76d2fc875a895addabeae2f8d30f0efc2",
      "0xedc81492a19ad70036b5a4614319953b8573776cabcaad99d6dd40d9b6d04104",
      "0x809440d9d16861009c8b7a29d5ba7614795dc04bf2f93406bcfee7c9bd4d90e6",
      "0x4dd3a286b76a19498348561413b039b0f06b80304ab611a7626f8bdae563faac",
      "0xca1f85a198bfa24c14540c618ea382ce032293c96fda02bd26172562162c48ae",
      "0x339b1d36192740791c587a310e00e64fdf15582e8248dd1330ab582063b77f7a",
      "0x74b2a883719b984d14bdabad5ff66b620b70511615455174ab5f550139451ee8",
      "0x87daa94884aff617678d16dee69a17f2cf62ebea182259d3cb3bd5052408757c",
      "0x9b4703d5eb9d2b0f06b9de954a80dc6c4cab40613888e73b42c1cffcd94d9afa",
      "0x42b0b4ac5ffec5134ff17b5815f339d5a325100b11c416c6538d692c4ef955b0",
      "0x2d689b1edfbdc716ed1b2e033fafc5cbbce218180c6645ff6287c72b1bf89fed",
      "0x39bec4dd14e64d98f3b83fd7b8155673b60ae4e31159d1e630a762004b4aefa9",
      "0xf999ef1013048e583ef8cc9c775728abea8f4544bfdf3c45f9ff3b59165fa1cb",
      "0xa4b4a10bda861d80dee7d71d939bc533471bfce707ce6bba556442af57008e36",
      "0xce742b16b17952e7488a6521cb49d685510fd15c29a7146b5caf3016361a704e",
      "0x241a3b0bca175fd7a6ac98d913ef37e74e11137ce54fb72cdba24b02680b0960",
      "0x28c8d78cca53f6d80565727b719ada89ea4d2d9454b0b32287b5c0dfce5e7dc3",
      "0xbef5f1c7ce2c624146d3d0c13d29b95c981de72e650341addeda6102fdff6e89",
      "0xdbd74877ad3f58578e0ec12cd1ad99c0b39edc453b0f39b17ff6c06e6d9655a9",
      "0xd03578f96d5992a505dcb6817dbe8da38afe2d3218577ce00b1864ab4a41fe65",
      "0x48de7c46f5c891e695726d6fdd03897da4de1d92b9863a17273cabb760199af9",
      "0x88807700ce049be08c741c433dbc4425960b8ee829b4fcb712f65418e3080048",
      "0x15b9900f7790e30eb463168d963f054661c5bb4dc97d8711f75d3bfdfa43f581",
      "0x3c4dad7aea767e1891a802ff6962b7478318dd24dced562c0242ec7cc580d121",
      "0x0d3d350a2c437575e9843b462106dd46c5a401ab0e6286125ddbe6b3e9d0a02c",
      "0x05d61ecde845c53f12e01ec9b68c836670aa84955f2b95a3a4d9a22642c517fb",
      "0xf6a0df1b00766e7f5d19b351007ca91fff37a3f2f96f7b8c7554faed7e726473",
      "0x47cc3ad00a0299d92819e150f14aa46e9e75e6c22be6a021b081fc0145e0f7c2",
      "0x43d80d8d17472ba4084d6afe21708cde56d7c5b3971801719fbf01bed393c1cb",
      "0xd31fcac68e0205d5990f0e00e1b6c4dad91d15dfd604f2893865d49a75278b99",
      "0x6c5428b564cc7431e3464b41b4c12a0618de66f17a3be08bd5321b10f492f65b",
      "0x843c5b10d22429e593abd34ea9bcfe8e6b2fd3c4e2e160135818292e3244a768",
      "0x9b435236fdd00e909865272010a0879e099381c915425247015bcb1855739ade",
      "0x5e9c62b268f114e0f95c09910997f493af53a9379c4e034f9a8d03ea08b1b7ab",
      "0x6593e2ae5374ba2b9068c05f6529217f9554d78a008ac2683fea1afd9cdfc2da",
      "0x5e707d48598bc3cc918711a2c94ec736d94f2cecda92d5aa3981e8c25aaec74a",
      "0x19e602075c6817cf8b7970fe7ec791caf529f99cd9ea17eba094db10bafcd779",
      "0x366e725bc6de56ada3675404dfe64a5ca4920619b6fc3d5626f144c73f1d072a",
      "0xd456bec29eb11471fb7e46a0d181e36b6e82e28dc6ab097755999039727ced58",
      "0x3c411579fc3719b6da42a2b473da708bfa8ed9acb1abf45c9f1fe0129302437d",
      "0x485dfe29537d03d0fbe941f155afae13d6e9d4b99aa3c7f12c7d95001c9887c9",
      "0xd072863cfed6389ec86f1feaf35830bab6f74507fa97af281d936e84703c4fce",
      "0xf7c0ebbf3381599b309383c7b6ed4179a7886157376277eb078d9a7a472be228",
      "0x18662c59c7ddadf21e5c28bdf6b64ecb0a69286e95f69cce8f533518591dabb7",
      "0xdaab150b170b6f490515ea3a06c7a15580b09b74bb34c072e60484c857ede975",
      "0xb27a17764453193414efff0ede91131be72e423794772aa29534a0a326b61bce",
      "0xb5285ec1b8018b0e26247d39e37a213d92f662b1e0bbcd6d29691a866777f6a4",
      "0xa78b47529a3dacee63d772d4fc3cf13efad0120a5563925d3dc600b710c51302",
      "0x92198c0e21f04ddd78cdc3eed49e40f8522f151e44f466204e8eda70fbb027f8",
      "0xacfcde1dea1a475b0b255ba2f1572901b71a6d5cfd5fa9039cf1c2e24b381a65",
      "0x51a8341eafc7c3abb8e8be4447a522fda7701ac70dbd9d25121617a4b1dcba1e",
      "0xc9890052530424b0cc66d4c590e51fdb902bbabc7713f7d4508229d0dfd5ddcb",
      "0x34be9c487fcfcf625d4dfb5bfe8051547f4668868fbe0bfa1b65c1d740778dc3",
      "0xa30b5f634ad9adbc02cdf918e0ab89cc8137f465219e66c0a11479018b908608",
      "0xee69246d143a95ad609781cc14a882a1eac1dba56254ea831bd4de1579ca2c33",
      "0x4a946c5e3f6a36b0f2dfc77fe91bc15267c90d7f03806f65bca2bdba6ecd9b36",
      "0x3dd93bc12c65741b93440479249d129087b3ca9e9e686d3bcbbf3fdafc888187",
      "0x82d5b0988910e64b8c3912596f419f599ffed1a74c3260b7c4b3734849b31bc0",
      "0xaad2672a3c645fa6eea46a06b7a307939b5fbab6a724438f73bb2466f1e9a53b",
      "0x0e0865565548a33910067406c76aad42581a0349889179a3fded8aa1bb307eba",
      "0xf69e2665627c1b20b6f6368a783c5a04e2eac5fec6587e25f7e229a4cff8b9c2",
      "0x0bb8d381fb363b96a4ac5523c951659ac9900a570d1ef0529e8556eb2a3aca2d",
      "0x0d39b71bb27e0c947cd57dabce9ed3df37a7ce5ceb1946c4017338361450b9a4",
      "0xca9d4d00b923d1aba2dfbcbaca0da9b46a2a144a7b1040b72bad8b40864d4f6e",
      "0x4143d1ab76ebda0871fbad8c8f57c9fe8cc4f6c501da09896e39f8faa835083e",
      "0x019f0ac0acc372b205030174a8a5c700590265e36b4f610eaab0d9fc7ed89901",
      "0x7f3f3872bbaa40d096abafab2eade430bc9539fe835220f7a3fa73741c311e3b",
      "0xf0c79b5992a1888fd094365482005f63a168cf99ea72f9e727a8770e2ccc7ce6",
      "0x6b80c9815a9513fe7aadb018892b3dd3dcfd43caed6aa5f34ab11b75dcdb74fd",
      "0x76a4af31c9eea72b9412225161a2211c87df8936b96ff318025e86762c975801",
      "0xf905d68caf4f30846c93f9b756f45a6eb61bbcddb4238a6f6175e5a85f33c5ad",
      "0x40e23aa380820033ae5aae8b15578de6cd69edb5481e7c4da9541cee96cf65ee",
      "0xe3589ca4d3d9d1b1a64c0ddc219b73723559a303b761ffb5ed25b0925bf3f586",
      "0xcc88bbb62909d1ad241aa42158efcc65c04251948b6dc69b11726fe07458f753",
      "0x4615b413adb071670037becd6a38ac3f1a2ae8b5a380c6d9e8cedccce15b4ba5",
      "0xbfaa23a269edadaa743eb29f0da14b4159c5b07e35d66e6db43dab9de0b597e6",
      "0x444b0c6092a5c829e573b6f2723b6bb22446532e963f88dabfc0535a718bda76",
      "0x2c9ae527b5a787c438b80424170878e8eff9dd06edf24021e2a336fe39162c1e",
      "0x815601a435b86db35658238509a69fe53ecb4295503dd7a815d198565af4b0d1",
      "0xd305faa29a8ac9bbe7fb569e2f5ade75ace91209a13f73968e9f1a778afde35f",
      "0x6ced5e05543b8c3be0b041945ced045541c8ba9b4efd047a10505b3ae73d877f",
      "0x46db11b6885177405f268be74900fd924a0dfd533b4da99384fa1b4e84e81399",
      "0x60a97b83783c2426aaeab3d71b364a1cb3e279ad9cb479c31a7b126194faaab8",
      "0x776cd04c677ad510eeb1c1e042f7c5307fcf8083e41fd382f0ecea01d9ad21d3",
      "0x4b63be05ca0d21603843c34dfac02b413d358fde354d3650edf8a42d9bcfd207",
      "0x7c740db2db40fe4a186d48ca20bf350e9dc65c996161e0f1f04e7915324f145f",
      "0x7909a765d4ebeb930158b220bf9cda1ca56caa2b9eaf1d5cfcaaf4e5a7a6f581",
      "0x270e09b65db2db522ea5b1c3b1281c5c0bec87ae2e343e2006f5301e485431ca",
      "0x06dd7b997cb45f2daa0e661e48f0047a8ddf27410a86aeb4d55bc40251788fbe",
      "0xafca750623733defb83bd7a4ca6615fffe766af08f95e47091098bed0ad4d56c",
      "0x9c2efa0f3817aba45915e66d4b4105e3b79d176b9b2000de5f2b12283683c4cf",
      "0x8c3bfd4eb2098623195b7e615ad8920592f8f7c391cc2811d9f97b7986578326",
      "0x07c7e8d42a1556d0aa339371e6da87c6c80bfa84b71c227c51d2e6a1e2bc62ce",
      "0x43b618514eee018515e3c43dc624908eb6bd63b570262388f8cccd6bf573bd7e",
      "0xa97e2f80fc9e2eed22436df5a37c002dfcdfb4e8244b8684fab82b2200409443",
      "0x9c4c2f5371f1d822158d1e27ec7129e6d5177b9ee12ba1973b22fae64f20fb33",
      "0x68b3d257c26a647bde380722a8e52fd048905c667cebf01ac0bb079bc9cf80b2",
      "0x36736a88171f5db366149e39fd45949dd635a007e913d8bee7f31246123cce3a",
      "0x745a64eec7daf0456a2b07cb608148540a02b56fb5861eeb473445758220dc08",
      "0xe0936844513451232707db4271a712ba7bb7a438fbfec58e571000d2ddb3e15a",
      "0x107cb9b2f1d6003f981b500b34d9cac863ffd2f9d7404664fe340d36053646d3",
      "0x7e7918074024c355af8ccd4663941d6c53ed4c6eabf0e5b83d6bc6c4973a9192",
      "0x5d825894f6334b6481b289b3293b73b8ec78303708db3230711c89a581a260f8",
      "0x3d3bd5ca75b71f81aa723d6507a29348096275d80c1b2c4f7f2230fe93f1f529",
      "0xebeb4ca7c620139dbc638e02da3f97972857c0760ee4ecc5b9e85f5cd2492fde",
      "0x15573495b527fac68d55777009a6c530a9db98d68523ce131ab1e1ff5e319a23",
      "0x46af0166b121b5ff20098e99cda5419fcc08334a00cd55fe68bf8bedb00596b3",
      "0xdfcd0b815846fa6c36c39b6a864462562ff2f7ef47ab64e2c7b074bd6c6825bd",
      "0xe108d2caa9d2169ee963f4be971a2030f762b40e6a4b202ed5e5a195ce55e6fd",
      "0x9276d962c663ca36a8b47bf316a35a568b8b1d9e703fb788810c3586f45bb345",
      "0xa98bbf6e28759d500fbd6be48fe58af486929f474a481907248b0e8358bc0ab4",
      "0x9f1cdd1cd0acb03a45178cda4d880907178e1bbac818168446c7cd857f741d99",
      "0x5d983a7484d024c503a2088d9db397cdc272c54bc843dc50fb2567b01f6bd024",
      "0x5d5ac5b677914617ed14444434bd60ea4d540c62a7447f9bcc16060b1fddce4a",
      "0xe1270abf35bf2f11343d892ac00054df4a5b3563a94178b3dd20274e687521d2",
      "0x437df0f77ea2390a0f0dc74e03fbb5624053b45ac6ebeb47b2821eed0fedd14f",
      "0x22fba27aaa0e355c7f1ce0f9c95a25ebd9707f8baa8b534dd932ea4cd18e4e80",
      "0x01eba0b313b90e72bef307cdbd8bdcc8f2fa0823c85665b6eb388113372e2086",
      "0xe0e7ca56c383141b324762861f7da67ac56981b9e5ebf29d0a274c4ccaea510b",
      "0xed57067f68e7b50e904c3a8463ff5b6e4ab90d5d5120aa196e7b8b17f1714378",
      "0x317033725020e2b48d2968b9f6ce3a5fbb091053ca46f7b3dcddba9ed91dacbb",
      "0x57aa336f58460dbe921bd6408f9f3d064189bbdea448fd145213f4c8771328c7",
      "0x18de8084261c5ddb807b1613d589a4835fabb6ff67b33af448d0ba287a6abc9f",
      "0xfabc2b90e2addbe9b42830a928e8377e9519a64173267405b0b03d66ec21dee3",
      "0x19339b28305f7c428567fa0a0a0167ffc2800f8479c4b55fa6d0bac1069fea45",
      "0x4e6634e35d850ddbccea085da6484a089fce3508a192b2b1087b0896519b6030",
      "0xeec6a9d6583abf18d44265d78022fd72b9a94fc4c7f019777faddc7af536ad57",
      "0xf5578de29a5cdd0c84c95de10256dfb6a155a9bfa721911e1a538a1a68141f3d",
      "0x1673fc133cc5e1f5ad4f335d756b0ec1a8db3b83059ae545d52a60522e2866c3"
    ]
  }
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Block information
Block object `OBJECT`

- **parentHash** `STRING` Parent block hash
- **sha3Uncles** `STRING` Ommers hash
- **miner** `STRING` Coinbase
- **stateRoot** `STRING` State root
- **transactionsRoot** `STRING` Transactions root
- **receiptsRoot** `STRING` Receipts root
- **logsBloom** `STRING` Bloom filter
- **difficulty** (_optional_) `STRING` Difficulty
- **number** `STRING` Number
- **gasLimit** `STRING` Gas limit
- **gasUsed** `STRING` Gas used
- **timestamp** `STRING` Timestamp
- **extraData** `STRING` Extra data
- **mixHash** `STRING` Mix hash
- **nonce** `STRING` Nonce
- **totalDifficulty** (_optional_) `STRING` Total difficult
- **baseFeePerGas** (_optional_) `STRING` Base fee per gas
- **size** `STRING` Block size
- **transactions** `ANYOF` of

  - Transaction hashes `ARRAY` of `STRING` 32 byte hex value

  - Full transactions `ARRAY` of

    - Signed 1559 Transaction `OBJECT`

      - **type** `STRING` type
      - **nonce** `STRING` nonce
      - **to** (_optional_) `STRING` to address
      - **gas** `STRING` gas limit
      - **value** `STRING` value
      - **input** `STRING` input data
      - **maxPriorityFeePerGas** `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
      - **maxFeePerGas** `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
      - **accessList** accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
        - **address** (_optional_) `STRING` hex encoded address
        - **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
      - **chainId** `STRING` chainId: Chain ID that this transaction is valid on.
      - **yParity** `STRING` yParity: The parity (0 for even, 1 for odd) of the y-value of the secp256k1 signature.
      - **r** `STRING` r
      - **s** `STRING` s

    - Signed 2930 Transaction `OBJECT`

      - **type** `STRING` type
      - **nonce** `STRING` nonce
      - **to** (_optional_) `STRING` to address
      - **gas** `STRING` gas limit
      - **value** `STRING` value
      - **input** `STRING` input data
      - **gasPrice** `STRING` gas price: The gas price willing to be paid by the sender in wei
      - **accessList** accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
        - **address** (_optional_) `STRING` hex encoded address
        - **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
      - **chainId** `STRING` chainId: Chain ID that this transaction is valid on.
      - **yParity** `STRING` yParity: The parity (0 for even, 1 for odd) of the y-value of the secp256k1 signature.
      - **r** `STRING` r
      - **s** `STRING` s

    - Signed Legacy Transaction `OBJECT`
      - **type** `STRING` type
      - **nonce** `STRING` nonce
      - **to** (_optional_) `STRING` to address
      - **gas** `STRING` gas limit
      - **value** `STRING` value
      - **input** `STRING` input data
      - **gasPrice** `STRING` gas price: The gas price willing to be paid by the sender in wei
      - **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.
      - **v** `STRING` v
      - **r** `STRING` r
      - **s** `STRING` s

- **uncles** Uncles `ARRAY` of `STRING` 32 byte hex value

## `eth_getBlockTransactionCountByHash`

Returns the number of transactions in a block from a block matching the given block hash.

[Brief version](detailed-json-rpc.md#eth_getBlockTransactionCountByHash)

**PARAMS**

1. **Block hash** (_optional_) `STRING` 32 byte hex value
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBlockTransactionCountByHash() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBlockTransactionCountByHash(
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBlockTransactionCountByHash();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0xa"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Transaction count
`STRING` hex encoded unsigned integer

## `eth_getBlockTransactionCountByNumber`

Returns the number of transactions in a block matching the given block number.

[Brief version](detailed-json-rpc.md#eth_getBlockTransactionCountByNumber)

**PARAMS**

1. **Block** (_optional_)

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByNumber",
  "params": ["latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByNumber",
  "params": [
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBlockTransactionCountByNumber() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBlockTransactionCountByNumber("latest");

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBlockTransactionCountByNumber();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0xba"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Transaction count
`STRING` hex encoded unsigned integer

## `eth_getUncleCountByBlockHash`

Returns the number of uncles in a block from a block matching the given block hash.

[Brief version](detailed-json-rpc.md#eth_getUncleCountByBlockHash)

**PARAMS**

1. **Block hash** (_optional_) `STRING` 32 byte hex value
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetUncleCountByBlockHash() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getUncleCountByBlockHash(
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetUncleCountByBlockHash();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Uncle count
`STRING` hex encoded unsigned integer

## `eth_getUncleCountByBlockNumber`

Returns the number of transactions in a block matching the given block number.

[Brief version](detailed-json-rpc.md#eth_getUncleCountByBlockNumber)

**PARAMS**

1. **Block** (_optional_)

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockNumber",
  "params": ["latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockNumber",
  "params": [
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetUncleCountByBlockNumber() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getUncleCountByBlockNumber("latest");

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetUncleCountByBlockNumber();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Uncle count
`STRING` hex encoded unsigned integer

## `eth_chainId`

Returns the chain ID of the current network.

[Brief version](detailed-json-rpc.md#eth_chainId)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_chainId",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_chainId",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runChainId() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_chainId();

  // Print the output to console
  console.log(result);
}

(async () => {
  runChainId();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x5"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Chain ID
`STRING` hex encoded unsigned integer

## `eth_syncing`

Returns an object with data about the sync status or false.

[Brief version](detailed-json-rpc.md#eth_syncing)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_syncing",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_syncing",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runSyncing() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_syncing();

  // Print the output to console
  console.log(result);
}

(async () => {
  runSyncing();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": false
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Syncing status
`ONEOF`

- Syncing progress `OBJECT`

  - **startingBlock** (_optional_) `STRING` Starting block
  - **currentBlock** (_optional_) `STRING` Current block
  - **highestBlock** (_optional_) `STRING` Highest block

- `BOOLEAN` Not syncing

## `eth_accounts`

Returns a list of addresses owned by client.

[Brief version](detailed-json-rpc.md#eth_accounts)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_accounts",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_accounts",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runAccounts() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_accounts();

  // Print the output to console
  console.log(result);
}

(async () => {
  runAccounts();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": []
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Accounts
`ARRAY` of `STRING` hex encoded address

## `eth_blockNumber`

Returns the number of most recent block.

[Brief version](detailed-json-rpc.md#eth_blockNumber)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_blockNumber",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_blockNumber",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runBlockNumber() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_blockNumber();

  // Print the output to console
  console.log(result);
}

(async () => {
  runBlockNumber();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x77f0f5"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Block number
`STRING` hex encoded unsigned integer

## `eth_call`

Executes a new message call immediately without creating a transaction on the block chain.

[Brief version](detailed-json-rpc.md#eth_call)

**PARAMS**

1. **Transaction** Transaction object generic to all types `OBJECT`

- **type** (_optional_) `STRING` type
- **nonce** (_optional_) `STRING` nonce
- **to** (_optional_) `STRING` to address
- **from** (_optional_) `STRING` from address
- **gas** (_optional_) `STRING` gas limit
- **value** (_optional_) `STRING` value
- **input** (_optional_) `STRING` input data
- **gasPrice** (_optional_) `STRING` gas price: The gas price willing to be paid by the sender in wei
- **maxPriorityFeePerGas** (_optional_) `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
- **maxFeePerGas** (_optional_) `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
- **accessList** (_optional_) accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
  - **address** (_optional_) `STRING` hex encoded address
  - **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
- **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.

1. **Block** (_optional_)

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_call",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    },
    "latest"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_call",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    },
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runCall() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_call(
    {
      from: "0x4469880099472dddfd357ab305ad2821d6e4647f",
      to: "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      gas: "0x4e3b29200",
      gasPrice: "0x89d12e6c0",
      value: "0x258689ac70a8000",
      data: "0x",
    },
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runCall();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

**RESULT**: Return data
`STRING` hex encoded bytes

## `eth_estimateGas`

Generates and returns an estimate of how much gas is necessary to allow the transaction to complete.

[Brief version](detailed-json-rpc.md#eth_estimateGas)

**PARAMS**

1. **Transaction** Transaction object generic to all types `OBJECT`

- **type** (_optional_) `STRING` type
- **nonce** (_optional_) `STRING` nonce
- **to** (_optional_) `STRING` to address
- **from** (_optional_) `STRING` from address
- **gas** (_optional_) `STRING` gas limit
- **value** (_optional_) `STRING` value
- **input** (_optional_) `STRING` input data
- **gasPrice** (_optional_) `STRING` gas price: The gas price willing to be paid by the sender in wei
- **maxPriorityFeePerGas** (_optional_) `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
- **maxFeePerGas** (_optional_) `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
- **accessList** (_optional_) accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
  - **address** (_optional_) `STRING` hex encoded address
  - **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
- **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.

1. **Block** (_optional_)

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_estimateGas",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    },
    "latest"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_estimateGas",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    },
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runEstimateGas() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_estimateGas(
    {
      from: "0x4469880099472dddfd357ab305ad2821d6e4647f",
      to: "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      gas: "0x4e3b29200",
      gasPrice: "0x89d12e6c0",
      value: "0x258689ac70a8000",
      data: "0x",
    },
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runEstimateGas();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

**RESULT**: Gas used
`STRING` hex encoded unsigned integer

## `eth_gasPrice`

Returns the current price per gas in wei.

[Brief version](detailed-json-rpc.md#eth_gasPrice)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_gasPrice",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_gasPrice",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGasPrice() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_gasPrice();

  // Print the output to console
  console.log(result);
}

(async () => {
  runGasPrice();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x11cf42d0d"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Gas price
`STRING` Gas price

## `eth_maxPriorityFeePerGas`

Returns the current maxPriorityFeePerGas per gas in wei.

[Brief version](detailed-json-rpc.md#eth_maxPriorityFeePerGas)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_maxPriorityFeePerGas",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_maxPriorityFeePerGas",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runMaxPriorityFeePerGas() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_maxPriorityFeePerGas();

  // Print the output to console
  console.log(result);
}

(async () => {
  runMaxPriorityFeePerGas();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x2700bfc"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Max priority fee per gas
`STRING` Max priority fee per gas

## `eth_feeHistory`

Transaction fee history

[Brief version](detailed-json-rpc.md#eth_feeHistory)

**PARAMS**

1. **blockCount**Requested range of blocks. Clients will return less than the requested range if not all blocks are available. `STRING` hex encoded unsigned integer

1. **newestBlock**Highest block of the requested range.

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

1. **rewardPercentiles**A monotonically increasing list of percentile values. For each block in the requested range, the transactions will be sorted in ascending order by effective tip per gas and the coresponding effective tip for the percentile will be determined, accounting for gas consumed. `ARRAY` of `NUMBER`NaN
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_feeHistory",
  "params": [2, "latest", []]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_feeHistory",
  "params": [
    2,
    "latest",
    []
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runFeeHistory() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_feeHistory(2, "latest", []);

  // Print the output to console
  console.log(result);
}

(async () => {
  runFeeHistory();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "oldestBlock": "0x77f0f5",
    "baseFeePerGas": ["0x1025a28ca", "0x11a842111", "0x1052393ae"],
    "gasUsedRatio": [0.8741241, 0.19733186666666666]
  }
}
```

{% endtab %}

{% endtabs %}

**RESULT**: feeHistoryResult
Fee history for the returned block range. This can be a subsection of the requested range if not all blocks are available.feeHistoryResults `OBJECT`

- **oldestBlock** `STRING` oldestBlock: Lowest number block of returned range.
- **baseFeePerGas** baseFeePerGasArray: An array of block base fees per gas. This includes the next block after the newest of the returned range, because this value can be derived from the newest block. Zeroes are returned for pre-EIP-1559 blocks. `ARRAY` of `STRING` hex encoded unsigned integer
- **reward** (_optional_) rewardArray: A two-dimensional array of effective priority fees per gas at the requested block percentiles. `ARRAY` of `ARRAY` of `STRING` rewardPercentile

## `eth_newFilter`

Creates a filter object, based on filter options, to notify when the state changes (logs).

[Brief version](detailed-json-rpc.md#eth_newFilter)

**PARAMS**

1. **Filter** (_optional_) filter `OBJECT`

- **fromBlock** (_optional_) `STRING` from block
- **toBlock** (_optional_) `STRING` to block
- **address** (_optional_) `ONEOF` of Address(es)

  - `STRING` Address

  - `ARRAY` of `STRING` hex encoded address

- **topics** (_optional_) Topics `ARRAY` of - `NULL`

      - `STRING` Single Topic Match

      - `ARRAY` of `STRING` 32 hex encoded bytes

  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newFilter",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newFilter",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runNewFilter() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_newFilter();

  // Print the output to console
  console.log(result);
}

(async () => {
  runNewFilter();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0xa6c212a33603d1d410d2d9f2ebe85a5201f174be99f1d356ac477097b21257a6"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Filter Identifier
`STRING` hex encoded unsigned integer

## `eth_newBlockFilter`

Creates a filter in the node, to notify when a new block arrives.

[Brief version](detailed-json-rpc.md#eth_newBlockFilter)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newBlockFilter",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newBlockFilter",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runNewBlockFilter() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_newBlockFilter();

  // Print the output to console
  console.log(result);
}

(async () => {
  runNewBlockFilter();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0xd6e71510dbb256f52d69057a6323f82e052b20833c81c1a8a8279a5e19c4c848"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Filter Identifier
`STRING` hex encoded unsigned integer

## `eth_uninstallFilter`

Uninstalls a filter with given id.

[Brief version](detailed-json-rpc.md#eth_uninstallFilter)

**PARAMS**

1. **Filter Identifier** (_optional_) `STRING` hex encoded unsigned integer
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_uninstallFilter",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_uninstallFilter",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runUninstallFilter() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_uninstallFilter();

  // Print the output to console
  console.log(result);
}

(async () => {
  runUninstallFilter();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

**RESULT**: Success
`BOOLEAN` undefined

## `eth_getFilterChanges`

Polling method for a filter, which returns an array of logs which occurred since last poll.

[Brief version](detailed-json-rpc.md#eth_getFilterChanges)

**PARAMS**

1. **Filter Identifier** (_optional_) `STRING` hex encoded unsigned integer
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterChanges",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterChanges",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetFilterChanges() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getFilterChanges();

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetFilterChanges();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

**RESULT**: Log objects
`ONEOF`

- `ARRAY` of `STRING` 32 byte hex value

- `ARRAY` of `STRING` 32 byte hex value

- `ARRAY` of log `OBJECT`
  - **removed** (_optional_) `BOOLEAN` removed
  - **logIndex** (_optional_) `STRING` log index
  - **transactionIndex** (_optional_) `STRING` transaction index
  - **transactionHash** `STRING` transaction hash
  - **blockHash** (_optional_) `STRING` block hash
  - **blockNumber** (_optional_) `STRING` block number
  - **address** (_optional_) `STRING` address
  - **data** (_optional_) `STRING` data
  - **topics** (_optional_) topics `ARRAY` of `STRING` 32 hex encoded bytes

## `eth_getFilterLogs`

Returns an array of all logs matching filter with given id.

[Brief version](detailed-json-rpc.md#eth_getFilterLogs)

**PARAMS**

1. **Filter Identifier** (_optional_) `STRING` hex encoded unsigned integer
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterLogs",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterLogs",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetFilterLogs() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getFilterLogs();

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetFilterLogs();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

**RESULT**: Log objects
`ONEOF`

- `ARRAY` of `STRING` 32 byte hex value

- `ARRAY` of `STRING` 32 byte hex value

- `ARRAY` of log `OBJECT`
  - **removed** (_optional_) `BOOLEAN` removed
  - **logIndex** (_optional_) `STRING` log index
  - **transactionIndex** (_optional_) `STRING` transaction index
  - **transactionHash** `STRING` transaction hash
  - **blockHash** (_optional_) `STRING` block hash
  - **blockNumber** (_optional_) `STRING` block number
  - **address** (_optional_) `STRING` address
  - **data** (_optional_) `STRING` data
  - **topics** (_optional_) topics `ARRAY` of `STRING` 32 hex encoded bytes

## `eth_getLogs`

Returns an array of all logs matching filter with given id.

[Brief version](detailed-json-rpc.md#eth_getLogs)

**PARAMS**

1. **Filter** (_optional_) filter `OBJECT`

- **fromBlock** (_optional_) `STRING` from block
- **toBlock** (_optional_) `STRING` to block
- **address** (_optional_) `ONEOF` of Address(es)

  - `STRING` Address

  - `ARRAY` of `STRING` hex encoded address

- **topics** (_optional_) Topics `ARRAY` of - `NULL`

      - `STRING` Single Topic Match

      - `ARRAY` of `STRING` 32 hex encoded bytes

  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getLogs",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getLogs",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetLogs() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getLogs();

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetLogs();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": [
    {
      "address": "0xdbb2b6c9a9efe247516d809a21a10d5341685797",
      "topics": [
        "0xb58a36f7ff42b62b489c2683fe31901c99b886003fec51eaf8c14f051d628374",
        "0x0000000000000000000000000000000000000000000000000000000000000002",
        "0x0000000000000000000000008a929789e58bf03011d93a9fce566e7536cfb32f"
      ],
      "data": "0x",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x11dcb16bcfc0d80a9ed7bba1971a758af32c3e21b7ee93f3a8edbf9021880dac",
      "transactionIndex": "0x0",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x0",
      "removed": false
    },
    {
      "address": "0x8efe26d6839108e831d3a37ca503ea4f136a8e73",
      "topics": [
        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
        "0x000000000000000000000000de9c3edff91c41c55c9a3d76632b4a95871d987e",
        "0x000000000000000000000000e08c99a3ccf28dad48c94a069f4492e55f1b818f"
      ],
      "data": "0x0000000000000000000000000000000000000000000000004563918244f40000",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xd38bbdc5252f1676a0b83a6a652bac734c4db0fbc4631e487b7e6dbe32357cbb",
      "transactionIndex": "0x1",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x1",
      "removed": false
    },
    {
      "address": "0x8efe26d6839108e831d3a37ca503ea4f136a8e73",
      "topics": [
        "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
        "0x000000000000000000000000de9c3edff91c41c55c9a3d76632b4a95871d987e",
        "0x000000000000000000000000e08c99a3ccf28dad48c94a069f4492e55f1b818f"
      ],
      "data": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xd38bbdc5252f1676a0b83a6a652bac734c4db0fbc4631e487b7e6dbe32357cbb",
      "transactionIndex": "0x1",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x2",
      "removed": false
    },
    {
      "address": "0x8efe26d6839108e831d3a37ca503ea4f136a8e73",
      "topics": [
        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
        "0x000000000000000000000000e08c99a3ccf28dad48c94a069f4492e55f1b818f",
        "0x0000000000000000000000000000000000000000000000000000000000000000"
      ],
      "data": "0x0000000000000000000000000000000000000000000000004563918244f40000",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xd38bbdc5252f1676a0b83a6a652bac734c4db0fbc4631e487b7e6dbe32357cbb",
      "transactionIndex": "0x1",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x3",
      "removed": false
    },
    {
      "address": "0xe08c99a3ccf28dad48c94a069f4492e55f1b818f",
      "topics": [
        "0x9e9794dbf94b0a0aa31a480f5b38550eda7f89115ac8fbf4953fa4dd219900c9",
        "0x0000000000000000000000008efe26d6839108e831d3a37ca503ea4f136a8e73",
        "0x000000000000000000000000de9c3edff91c41c55c9a3d76632b4a95871d987e"
      ],
      "data": "0x00000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000004563918244f40000000000000000000000000000000000000000000000000000000000000000c804000000000000000000000000000000000000000000000000000000000000002c6f6e6f6d7931367970786361677568326d787a716635796e6865677361656e737563687865396e6e73346d660000000000000000000000000000000000000000",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xd38bbdc5252f1676a0b83a6a652bac734c4db0fbc4631e487b7e6dbe32357cbb",
      "transactionIndex": "0x1",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x4",
      "removed": false
    },
    {
      "address": "0x326c977e6efc84e512bb9c30f76e30c160ed06fb",
      "topics": [
        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
        "0x0000000000000000000000004281ecf07378ee595c564a59048801330f3084ee",
        "0x000000000000000000000000e25ba8ec283a86a3dbfb471ec262e26dd8137c59"
      ],
      "data": "0x000000000000000000000000000000000000000000000001158e460913d00000",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xf689203650170c9e928160bb25fc83eeef50df0e437a440ce6a0475b04ac85b3",
      "transactionIndex": "0x4",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x5",
      "removed": false
    },
    {
      "address": "0x326c977e6efc84e512bb9c30f76e30c160ed06fb",
      "topics": [
        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
        "0x0000000000000000000000004281ecf07378ee595c564a59048801330f3084ee",
        "0x000000000000000000000000eb2cb332c82b874c3a755e7cf31ac400512be6d6"
      ],
      "data": "0x000000000000000000000000000000000000000000000001158e460913d00000",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x9bb2ba889d24327731544d4af097e039d77bd2de6960e2be21ad4ce8d44af8f6",
      "transactionIndex": "0x6",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x6",
      "removed": false
    },
    {
      "address": "0x6df799e080759604d07da4a4595128373beb5d81",
      "topics": [
        "0xb8b9c39aeba1cfd98c38dfeebe11c2f7e02b334cbe9f05f22b442a5d9c1ea0c5"
      ],
      "data": "0x12b592d666e86503574e5c1ef764617ad36ccce8a8dbbd9d55fef02f19640b7f0eceb89e6923e05d447e528262aeea6fb4498037b210154a57b52b0476ee96920272f83fc6e09395438868cb1fba743e3d6b130d5fb427be27c2938066ab8251",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x79f84471585c1de75bfc6b012d2190c0ebd797ef0fb6859aba44970a9eb1d037",
      "transactionIndex": "0x11",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x7",
      "removed": false
    },
    {
      "address": "0x6df799e080759604d07da4a4595128373beb5d81",
      "topics": [
        "0xb8b9c39aeba1cfd98c38dfeebe11c2f7e02b334cbe9f05f22b442a5d9c1ea0c5"
      ],
      "data": "0xdc45e31ca61b9fda1587cdee722a07d01f3ae45786ccf11a389d2233c184f36416d2dd0c8d1e7ba80eac27d98dc038fcc0388788279f2ef05f84bfb1b01a2cfa058c755709d2b0d0411a13fc8434a9c2d6f05f98385609f573152234903ef02b",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x39cf2d6e7340eb13ad8cbcb182707eb9432a7618d4b432aba6a897774cb07658",
      "transactionIndex": "0x12",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x8",
      "removed": false
    },
    {
      "address": "0x6df799e080759604d07da4a4595128373beb5d81",
      "topics": [
        "0x98fd0d40bd3e226c28fb29ff2d386bd8f9e19f2f8436441e6b854651d3b687b3"
      ],
      "data": "0xc34cd2e329f17ac8554c101cfcd7278e67ca94d1d3d20ea8daab159eafb52525c5e23fb2b03d63655eb912f89bb5dab1e4841b35f68de4c16381e2a2e971f44a038df4328ffdc7338c7214a3aa36cea3c98718317ee7ba8cd6efa4affb533d55",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x703577606d12267c143f4198e0e297fdccaea45c16f4ca2cf8cd2235da4fa18a",
      "transactionIndex": "0x13",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x9",
      "removed": false
    },
    {
      "address": "0x8b6147ebb2623369cd2dbc4cad3f36e2828c423c",
      "topics": [
        "0x73b132cb33951232d83dc0f1f81c2d10f9a2598f057404ed02756716092097bb"
      ],
      "data": "0xb3c95bccd011917fae0afc7780432b55be773914ba20f089be06a3802cc112f9000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000020eceb89e6923e05d447e528262aeea6fb4498037b210154a57b52b0476ee969216d2dd0c8d1e7ba80eac27d98dc038fcc0388788279f2ef05f84bfb1b01a2cfa",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x703577606d12267c143f4198e0e297fdccaea45c16f4ca2cf8cd2235da4fa18a",
      "transactionIndex": "0x13",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0xa",
      "removed": false
    },
    {
      "address": "0xfe76edf35648cc733d57200646cb1dc63d05462f",
      "topics": [
        "0x9866f8ddfe70bb512b2f2b28b49d4017c43f7ba775f1a20c61c13eea8cdac111"
      ],
      "data": "0xb3c95bccd011917fae0afc7780432b55be773914ba20f089be06a3802cc112f9",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xc01e728ebf8771028b571c00ed8cd4179deff43903f090a6fd7012412805adb4",
      "transactionIndex": "0x14",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0xb",
      "removed": false
    },
    {
      "address": "0xfe76edf35648cc733d57200646cb1dc63d05462f",
      "topics": [
        "0x2672b53d25204094519f7b0fba8d2b5cd0cc1e426f49554c89461cdb9dcec08f"
      ],
      "data": "0x00000000000000000000000000000000000000000000000000000000000014270000000000000000000000000000000000000000000000000000000000001427",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xc01e728ebf8771028b571c00ed8cd4179deff43903f090a6fd7012412805adb4",
      "transactionIndex": "0x14",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0xc",
      "removed": false
    },
    {
      "address": "0x52bc93129d4defc04c7aef6135fcae26abc047cc",
      "topics": [
        "0x955d4d39a5ccb8ff2d5a3d8508cb233a43a4f67441f1fe3b7d3a20007978811f",
        "0x0000000000000000000000009eda8333e09828571db26576a566668f79f98946"
      ],
      "data": "0x000000000000000000000000000000000000000000000000000000000076dc06000000000000000000000000000000000000000000000000000000000077f0f6000000000000000000000000000000000000000000000000000000000077f095000000000000000000000000000000000000000000000000000000000000007000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000000",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x3c9fae743c1a94430035527a73434f156e2f54a426e6a210580803748fcfad89",
      "transactionIndex": "0x15",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0xd",
      "removed": false
    },
    {
      "address": "0x233a95ccebf3c9f934482c637c08b4015cdd6ddd",
      "topics": [
        "0x29233ba1d7b302b8fe230ad0b81423aba5371b2a6f6b821228212385ee6a4420",
        "0xcb87d1d8035f65acd081bab0ed0b65805aeaef7fe67293a7b4157129a28911a5",
        "0x0000000000000000000000000000000000000000000000000000000000000001"
      ],
      "data": "0x000000000000000000000000000000000000000000000000000000000077f0f3000000000000000000000000000000000000000000000000000000000000d9f7000000000000000000000000000000000000000000000000000000000001382200000000000000000000000000000000000000000000000002b0441ebe2850fd",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x3c9fae743c1a94430035527a73434f156e2f54a426e6a210580803748fcfad89",
      "transactionIndex": "0x15",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0xe",
      "removed": false
    },
    {
      "address": "0xcc7bb2d219a0fc08033e130629c2b854b7ba9195",
      "topics": [
        "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
        "0x0000000000000000000000006b55bc5ac92f83b4179a83a797a64e35c885e1f0",
        "0x000000000000000000000000805fe47d1fe7d86496753bb4b36206953c1ae660"
      ],
      "data": "0x0000000000000000000000000000000000000000000000002c68af0bb1400000",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xfa81695d7e084eed9ee9a0f19b40674f4960a62a13333a1bdf89bccca4e8ef6e",
      "transactionIndex": "0x16",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0xf",
      "removed": false
    },
    {
      "address": "0xca41f293a32d25c2216bc4b30f5b0ab61b6ed2cb",
      "topics": [
        "0xe9149e1b5059238baed02fa659dbf4bd932fbcf760a431330df4d934bc942f37",
        "0x00000000000000000000000037f922217a6612f142d5e7ce0ba0d6a4c2471ddf"
      ],
      "data": "0x000000000000000000000000000000000000000000000000000000000000006400000000000000000000000000000000000000000000000000000000000065e2",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0xee3022450c1174fbc4f5ab9c29a0d9b88c7ecfa35d45c934073972513502c5f2",
      "transactionIndex": "0x18",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x10",
      "removed": false
    },
    {
      "address": "0x8e329c262b0876450178f107cdadbf3b364d6560",
      "topics": [
        "0xef87e24294defbf647d4ce97e9905a82d73c6e9e03417521acc5ba4aeaf1d618"
      ],
      "data": "0x000000000000000000000000000000000000000000000000000000000000753a000000000000000000000000b589178adfb6c6915c55b08b284bdbbbcf4f452e",
      "blockNumber": "0x77f0f6",
      "transactionHash": "0x705a92388b5738fe776ca3daeb4eef6301b030cc6ac2e6c46bd13b272d8ad017",
      "transactionIndex": "0x1a",
      "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
      "logIndex": "0x11",
      "removed": false
    }
  ]
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Log objects
`ONEOF`

- `ARRAY` of `STRING` 32 byte hex value

- `ARRAY` of `STRING` 32 byte hex value

- `ARRAY` of log `OBJECT`
  - **removed** (_optional_) `BOOLEAN` removed
  - **logIndex** (_optional_) `STRING` log index
  - **transactionIndex** (_optional_) `STRING` transaction index
  - **transactionHash** `STRING` transaction hash
  - **blockHash** (_optional_) `STRING` block hash
  - **blockNumber** (_optional_) `STRING` block number
  - **address** (_optional_) `STRING` address
  - **data** (_optional_) `STRING` data
  - **topics** (_optional_) topics `ARRAY` of `STRING` 32 hex encoded bytes

## `eth_mining`

Returns whether the client is actively mining new blocks.

[Brief version](detailed-json-rpc.md#eth_mining)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_mining",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_mining",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runMining() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_mining();

  // Print the output to console
  console.log(result);
}

(async () => {
  runMining();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": false
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Mining status
`BOOLEAN` miningStatus

## `eth_hashrate`

Returns the number of hashes per second that the node is mining with.

[Brief version](detailed-json-rpc.md#eth_hashrate)

**PARAMS**

none
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_hashrate",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_hashrate",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runHashrate() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_hashrate();

  // Print the output to console
  console.log(result);
}

(async () => {
  runHashrate();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Mining status
`STRING` Hashrate

## `eth_getBalance`

Returns the balance of the account of given address.

[Brief version](detailed-json-rpc.md#eth_getBalance)

**PARAMS**

1. **Address** `STRING` hex encoded address

1. **Block** (_optional_)

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBalance",
  "params": ["0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b", "latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBalance",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBalance() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBalance(
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBalance();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Balance
`STRING` hex encoded unsigned integer

## `eth_getStorageAt`

Returns the value from a storage position at a given address.

[Brief version](detailed-json-rpc.md#eth_getStorageAt)

**PARAMS**

1. **Address** `STRING` hex encoded address

1. **Storage slot** `STRING` hex encoded unsigned integer

1. **Block** (_optional_)

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getStorageAt",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "0x0000000000000000000000000000000000000000000000000000000000000001",
    "latest"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getStorageAt",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "0x0000000000000000000000000000000000000000000000000000000000000001",
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetStorageAt() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getStorageAt(
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "0x0000000000000000000000000000000000000000000000000000000000000001",
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetStorageAt();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0000000000000000000000000000000000000000000000000000000000000000"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Value
`STRING` hex encoded bytes

## `eth_getTransactionCount`

Returns the number of transactions sent from an address.

[Brief version](detailed-json-rpc.md#eth_getTransactionCount)

**PARAMS**

1. **Address** `STRING` hex encoded address

1. **Block** (_optional_)

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionCount",
  "params": ["0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b", "latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionCount",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionCount() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionCount(
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionCount();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x1"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Transaction count
`STRING` hex encoded unsigned integer

## `eth_getCode`

Returns code at a given address.

[Brief version](detailed-json-rpc.md#eth_getCode)

**PARAMS**

1. **Address** `STRING` hex encoded address

1. **Block** (_optional_)

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
  {% tabs %}
  {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getCode",
  "params": ["0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b", "latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getCode",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetCode() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getCode(
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetCode();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x6080604052600436106100e15760003560e01c806380f59a651161007f578063c01a8c8411610059578063c01a8c8414610349578063c642747414610372578063d0549b851461039b578063ee22610b146103c657610138565b806380f59a65146102a05780639ace38c2146102dd578063a0e67e2b1461031e57610138565b806320ea8d86116100bb57806320ea8d86146101ce5780632e7700f0146101f75780632f54bf6e1461022257806333ea3dc81461025f57610138565b8063025e7c271461013d57806306fdde031461017a5780630bc0fe8f146101a557610138565b36610138573373ffffffffffffffffffffffffffffffffffffffff167f90890809c654f11d6e72a28fa60149770a0d11ec6c92319d6ceb2bb0a4ea1a15344760405161012e929190611704565b60405180910390a2005b600080fd5b34801561014957600080fd5b50610164600480360381019061015f919061176d565b6103ef565b60405161017191906117db565b60405180910390f35b34801561018657600080fd5b5061018f61042e565b60405161019c919061188f565b60405180910390f35b3480156101b157600080fd5b506101cc60048036038101906101c79190611a25565b61046b565b005b3480156101da57600080fd5b506101f560048036038101906101f0919061176d565b61086e565b005b34801561020357600080fd5b5061020c610b48565b6040516102199190611a81565b60405180910390f35b34801561022e57600080fd5b5061024960048036038101906102449190611a9c565b610b55565b6040516102569190611ae4565b60405180910390f35b34801561026b57600080fd5b506102866004803603810190610281919061176d565b610b75565b604051610297959493929190611b54565b60405180910390f35b3480156102ac57600080fd5b506102c760048036038101906102c29190611bae565b610c88565b6040516102d49190611ae4565b60405180910390f35b3480156102e957600080fd5b5061030460048036038101906102ff919061176d565b610cb7565b604051610315959493929190611b54565b60405180910390f35b34801561032a57600080fd5b50610333610db2565b6040516103409190611cac565b60405180910390f35b34801561035557600080fd5b50610370600480360381019061036b919061176d565b610e40565b005b34801561037e57600080fd5b5061039960048036038101906103949190611d83565b61111d565b005b3480156103a757600080fd5b506103b0611327565b6040516103bd9190611a81565b60405180910390f35b3480156103d257600080fd5b506103ed60048036038101906103e8919061176d565b61132d565b005b600181815481106103ff57600080fd5b906000526020600020016000915054906101000a900473ffffffffffffffffffffffffffffffffffffffff1681565b60606040518060400160405280600e81526020017f4d756c746953696757616c6c6574000000000000000000000000000000000000815250905090565b60008060019054906101000a900460ff1615905080801561049c5750600160008054906101000a900460ff1660ff16105b806104c957506104ab30611625565b1580156104c85750600160008054906101000a900460ff1660ff16145b5b610508576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016104ff90611e64565b60405180910390fd5b60016000806101000a81548160ff021916908360ff1602179055508015610545576001600060016101000a81548160ff0219169083151502179055505b7f63a242a632efe33c0e210e04e4173612a17efa4f16aa4890bc7e46caece80de0600a6040516105759190611ec9565b60405180910390a160008351116105c1576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016105b890611f30565b60405180910390fd5b6000821180156105d2575082518211155b610611576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040161060890611fc2565b60405180910390fd5b60005b835181101561080857600084828151811061063257610631611fe2565b5b60200260200101519050600073ffffffffffffffffffffffffffffffffffffffff168173ffffffffffffffffffffffffffffffffffffffff1614156106ac576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016106a39061205d565b60405180910390fd5b600260008273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff1615610739576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610730906120c9565b60405180910390fd5b6001600260008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff0219169083151502179055506001819080600181540180825580915050600190039060005260206000200160009091909190916101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555050808061080090612118565b915050610614565b508160038190555080156108695760008060016101000a81548160ff0219169083151502179055507f7f26b83ff96e1f2b6a682f133852f6798a09c465da95921460cefb3847402498600160405161086091906121a9565b60405180910390a15b505050565b600260003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff166108fa576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016108f190612210565b60405180910390fd5b806005805490508110610942576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016109399061227c565b60405180910390fd5b816005818154811061095757610956611fe2565b5b906000526020600020906005020160030160009054906101000a900460ff16156109b6576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016109ad906122e8565b60405180910390fd5b6000600584815481106109cc576109cb611fe2565b5b906000526020600020906005020190506004600085815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff16610a79576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610a7090612354565b60405180910390fd5b6001816004016000828254610a8e9190612374565b9250508190555060006004600086815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff021916908315150217905550833373ffffffffffffffffffffffffffffffffffffffff167fc423fd18c78c483f167229efa90b29abe30eed1425ab9cb40441f6555650eca860405160405180910390a350505050565b6000600580549050905090565b60026020528060005260406000206000915054906101000a900460ff1681565b6000806060600080600060058781548110610b9357610b92611fe2565b5b906000526020600020906005020190508060000160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff168160010154826002018360030160009054906101000a900460ff168460040154828054610bf4906123d7565b80601f0160208091040260200160405190810160405280929190818152602001828054610c20906123d7565b8015610c6d5780601f10610c4257610100808354040283529160200191610c6d565b820191906000526020600020905b815481529060010190602001808311610c5057829003601f168201915b50505050509250955095509550955095505091939590929450565b60046020528160005260406000206020528060005260406000206000915091509054906101000a900460ff1681565b60058181548110610cc757600080fd5b90600052602060002090600502016000915090508060000160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1690806001015490806002018054610d16906123d7565b80601f0160208091040260200160405190810160405280929190818152602001828054610d42906123d7565b8015610d8f5780601f10610d6457610100808354040283529160200191610d8f565b820191906000526020600020905b815481529060010190602001808311610d7257829003601f168201915b5050505050908060030160009054906101000a900460ff16908060040154905085565b60606001805480602002602001604051908101604052809291908181526020018280548015610e3657602002820191906000526020600020905b8160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019060010190808311610dec575b5050505050905090565b600260003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff16610ecc576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610ec390612210565b60405180910390fd5b806005805490508110610f14576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610f0b9061227c565b60405180910390fd5b8160058181548110610f2957610f28611fe2565b5b906000526020600020906005020160030160009054906101000a900460ff1615610f88576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610f7f906122e8565b60405180910390fd5b826004600082815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff1615611027576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040161101e90612455565b60405180910390fd5b60006005858154811061103d5761103c611fe2565b5b9060005260206000209060050201905060018160040160008282546110629190612475565b9250508190555060016004600087815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff021916908315150217905550843373ffffffffffffffffffffffffffffffffffffffff167f52a3954c699324c8e90e7e2f7cb9f57cd61af1902197bafcc5085b6c2a57b82360405160405180910390a35050505050565b600260003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff166111a9576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016111a090612210565b60405180910390fd5b6000600580549050905060056040518060a001604052808673ffffffffffffffffffffffffffffffffffffffff1681526020018581526020018481526020016000151581526020016000815250908060018154018082558091505060019003906000526020600020906005020160009091909190915060008201518160000160006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555060208201518160010155604082015181600201908051906020019061128c929190611648565b5060608201518160030160006101000a81548160ff0219169083151502179055506080820151816004015550508373ffffffffffffffffffffffffffffffffffffffff16813373ffffffffffffffffffffffffffffffffffffffff167f52e5c631bb2fd786d6b1c26f68548e07c61d087bf325770dd88d072cf0a5e8b086866040516113199291906124cb565b60405180910390a450505050565b60035481565b600260003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff166113b9576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016113b090612210565b60405180910390fd5b806005805490508110611401576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016113f89061227c565b60405180910390fd5b816005818154811061141657611415611fe2565b5b906000526020600020906005020160030160009054906101000a900460ff1615611475576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040161146c906122e8565b60405180910390fd5b60006005848154811061148b5761148a611fe2565b5b90600052602060002090600502019050600354816004015410156114e4576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016114db90612547565b60405180910390fd5b60018160030160006101000a81548160ff02191690831515021790555060008160000160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168260010154836002016040516115549190612606565b60006040518083038185875af1925050503d8060008114611591576040519150601f19603f3d011682016040523d82523d6000602084013e611596565b606091505b50509050806115da576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016115d190612669565b60405180910390fd5b843373ffffffffffffffffffffffffffffffffffffffff167f5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac60405160405180910390a35050505050565b6000808273ffffffffffffffffffffffffffffffffffffffff163b119050919050565b828054611654906123d7565b90600052602060002090601f01602090048101928261167657600085556116bd565b82601f1061168f57805160ff19168380011785556116bd565b828001600101855582156116bd579182015b828111156116bc5782518255916020019190600101906116a1565b5b5090506116ca91906116ce565b5090565b5b808211156116e75760008160009055506001016116cf565b5090565b6000819050919050565b6116fe816116eb565b82525050565b600060408201905061171960008301856116f5565b61172660208301846116f5565b9392505050565b6000604051905090565b600080fd5b600080fd5b61174a816116eb565b811461175557600080fd5b50565b60008135905061176781611741565b92915050565b60006020828403121561178357611782611737565b5b600061179184828501611758565b91505092915050565b600073ffffffffffffffffffffffffffffffffffffffff82169050919050565b60006117c58261179a565b9050919050565b6117d5816117ba565b82525050565b60006020820190506117f060008301846117cc565b92915050565b600081519050919050565b600082825260208201905092915050565b60005b83811015611830578082015181840152602081019050611815565b8381111561183f576000848401525b50505050565b6000601f19601f8301169050919050565b6000611861826117f6565b61186b8185611801565b935061187b818560208601611812565b61188481611845565b840191505092915050565b600060208201905081810360008301526118a98184611856565b905092915050565b600080fd5b7f4e487b7100000000000000000000000000000000000000000000000000000000600052604160045260246000fd5b6118ee82611845565b810181811067ffffffffffffffff8211171561190d5761190c6118b6565b5b80604052505050565b600061192061172d565b905061192c82826118e5565b919050565b600067ffffffffffffffff82111561194c5761194b6118b6565b5b602082029050602081019050919050565b600080fd5b61196b816117ba565b811461197657600080fd5b50565b60008135905061198881611962565b92915050565b60006119a161199c84611931565b611916565b905080838252602082019050602084028301858111156119c4576119c361195d565b5b835b818110156119ed57806119d98882611979565b8452602084019350506020810190506119c6565b5050509392505050565b600082601f830112611a0c57611a0b6118b1565b5b8135611a1c84826020860161198e565b91505092915050565b60008060408385031215611a3c57611a3b611737565b5b600083013567ffffffffffffffff811115611a5a57611a5961173c565b5b611a66858286016119f7565b9250506020611a7785828601611758565b9150509250929050565b6000602082019050611a9660008301846116f5565b92915050565b600060208284031215611ab257611ab1611737565b5b6000611ac084828501611979565b91505092915050565b60008115159050919050565b611ade81611ac9565b82525050565b6000602082019050611af96000830184611ad5565b92915050565b600081519050919050565b600082825260208201905092915050565b6000611b2682611aff565b611b308185611b0a565b9350611b40818560208601611812565b611b4981611845565b840191505092915050565b600060a082019050611b6960008301886117cc565b611b7660208301876116f5565b8181036040830152611b888186611b1b565b9050611b976060830185611ad5565b611ba460808301846116f5565b9695505050505050565b60008060408385031215611bc557611bc4611737565b5b6000611bd385828601611758565b9250506020611be485828601611979565b9150509250929050565b600081519050919050565b600082825260208201905092915050565b6000819050602082019050919050565b611c23816117ba565b82525050565b6000611c358383611c1a565b60208301905092915050565b6000602082019050919050565b6000611c5982611bee565b611c638185611bf9565b9350611c6e83611c0a565b8060005b83811015611c9f578151611c868882611c29565b9750611c9183611c41565b925050600181019050611c72565b5085935050505092915050565b60006020820190508181036000830152611cc68184611c4e565b905092915050565b600080fd5b600067ffffffffffffffff821115611cee57611ced6118b6565b5b611cf782611845565b9050602081019050919050565b82818337600083830152505050565b6000611d26611d2184611cd3565b611916565b905082815260208101848484011115611d4257611d41611cce565b5b611d4d848285611d04565b509392505050565b600082601f830112611d6a57611d696118b1565b5b8135611d7a848260208601611d13565b91505092915050565b600080600060608486031215611d9c57611d9b611737565b5b6000611daa86828701611979565b9350506020611dbb86828701611758565b925050604084013567ffffffffffffffff811115611ddc57611ddb61173c565b5b611de886828701611d55565b9150509250925092565b7f496e697469616c697a61626c653a20636f6e747261637420697320616c72656160008201527f647920696e697469616c697a6564000000000000000000000000000000000000602082015250565b6000611e4e602e83611801565b9150611e5982611df2565b604082019050919050565b60006020820190508181036000830152611e7d81611e41565b9050919050565b6000819050919050565b6000819050919050565b6000611eb3611eae611ea984611e84565b611e8e565b6116eb565b9050919050565b611ec381611e98565b82525050565b6000602082019050611ede6000830184611eba565b92915050565b7f6f776e6572732072657175697265640000000000000000000000000000000000600082015250565b6000611f1a600f83611801565b9150611f2582611ee4565b602082019050919050565b60006020820190508181036000830152611f4981611f0d565b9050919050565b7f696e76616c6964206e756d626572206f6620726571756972656420636f6e666960008201527f726d6174696f6e73000000000000000000000000000000000000000000000000602082015250565b6000611fac602883611801565b9150611fb782611f50565b604082019050919050565b60006020820190508181036000830152611fdb81611f9f565b9050919050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052603260045260246000fd5b7f696e76616c6964206f776e657200000000000000000000000000000000000000600082015250565b6000612047600d83611801565b915061205282612011565b602082019050919050565b600060208201905081810360008301526120768161203a565b9050919050565b7f6f776e6572206e6f7420756e6971756500000000000000000000000000000000600082015250565b60006120b3601083611801565b91506120be8261207d565b602082019050919050565b600060208201905081810360008301526120e2816120a6565b9050919050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052601160045260246000fd5b6000612123826116eb565b91507fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff821415612156576121556120e9565b5b600182019050919050565b6000819050919050565b600060ff82169050919050565b600061219361218e61218984612161565b611e8e565b61216b565b9050919050565b6121a381612178565b82525050565b60006020820190506121be600083018461219a565b92915050565b7f6e6f74206f776e65720000000000000000000000000000000000000000000000600082015250565b60006121fa600983611801565b9150612205826121c4565b602082019050919050565b60006020820190508181036000830152612229816121ed565b9050919050565b7f747820646f6573206e6f74206578697374000000000000000000000000000000600082015250565b6000612266601183611801565b915061227182612230565b602082019050919050565b6000602082019050818103600083015261229581612259565b9050919050565b7f747820616c726561647920657865637574656400000000000000000000000000600082015250565b60006122d2601383611801565b91506122dd8261229c565b602082019050919050565b60006020820190508181036000830152612301816122c5565b9050919050565b7f7478206e6f7420636f6e6669726d656400000000000000000000000000000000600082015250565b600061233e601083611801565b915061234982612308565b602082019050919050565b6000602082019050818103600083015261236d81612331565b9050919050565b600061237f826116eb565b915061238a836116eb565b92508282101561239d5761239c6120e9565b5b828203905092915050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052602260045260246000fd5b600060028204905060018216806123ef57607f821691505b60208210811415612403576124026123a8565b5b50919050565b7f747820616c726561647920636f6e6669726d6564000000000000000000000000600082015250565b600061243f601483611801565b915061244a82612409565b602082019050919050565b6000602082019050818103600083015261246e81612432565b9050919050565b6000612480826116eb565b915061248b836116eb565b9250827fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff038211156124c0576124bf6120e9565b5b828201905092915050565b60006040820190506124e060008301856116f5565b81810360208301526124f28184611b1b565b90509392505050565b7f63616e6e6f742065786563757465207478000000000000000000000000000000600082015250565b6000612531601183611801565b915061253c826124fb565b602082019050919050565b6000602082019050818103600083015261256081612524565b9050919050565b600081905092915050565b60008190508160005260206000209050919050565b60008154612594816123d7565b61259e8186612567565b945060018216600081146125b957600181146125ca576125fd565b60ff198316865281860193506125fd565b6125d385612572565b60005b838110156125f5578154818901526001820191506020810190506125d6565b838801955050505b50505092915050565b60006126128284612587565b915081905092915050565b7f7478206661696c65640000000000000000000000000000000000000000000000600082015250565b6000612653600983611801565b915061265e8261261d565b602082019050919050565b6000602082019050818103600083015261268281612646565b905091905056fea26469706673582212206c9d550f615a6cc987e89a94b4f4b6d7be4c8c2da4ace7b55292611c528f9a8864736f6c63430008090033"
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Bytecode
`STRING` hex encoded bytes

## `eth_sendRawTransaction`

Submits a raw transaction.

[Brief version](detailed-json-rpc.md#eth_sendRawTransaction)

**PARAMS**

1. **Transaction** `STRING` hex encoded bytes
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_sendRawTransaction",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    }
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_sendRawTransaction",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    }
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runSendRawTransaction() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_sendRawTransaction({
    from: "0x4469880099472dddfd357ab305ad2821d6e4647f",
    to: "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
    gas: "0x4e3b29200",
    gasPrice: "0x89d12e6c0",
    value: "0x258689ac70a8000",
    data: "0x",
  });

  // Print the output to console
  console.log(result);
}

(async () => {
  runSendRawTransaction();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

**RESULT**: Transaction hash
`STRING` 32 byte hex value

## `eth_getTransactionByHash`

Returns the information about a transaction requested by transaction hash.

[Brief version](detailed-json-rpc.md#eth_getTransactionByHash)

**PARAMS**

1. **Transaction hash** `STRING` 32 byte hex value
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByHash",
  "params": [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByHash",
  "params": [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionByHash() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionByHash(
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionByHash();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "blockHash": "0xb39de02094847558d1b5b7be17899af87d4026419f063946d347aeb4b8f17b56",
    "blockNumber": "0x7787e4",
    "transactionIndex": "0x24",
    "hash": "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188",
    "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
    "to": "0xd9ded92319814d8f3587dfad7be72ca71e16697a",
    "input": "0xee22610b0000000000000000000000000000000000000000000000000000000000000000",
    "nonce": "0x17",
    "value": "0x0",
    "gas": "0xf4240",
    "gasPrice": "0x9a26693e",
    "maxPriorityFeePerGas": "0x59682f00",
    "maxFeePerGas": "0xab58f0b6",
    "accessList": [],
    "chainId": "0x5",
    "type": "0x2",
    "v": "0x1",
    "r": "0x1a54710a2409beff5e5726830497f9f56f0ae1545c25b4436d8ac8d68900c2e8",
    "s": "0x5b6b60bbb030b1f88d098252d98b4731d7e89d6b1a8b2e7dee61c2ea45866f29"
  }
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Transaction information
Transaction information `OBJECT`

- **blockHash** `STRING` block hash
- **blockNumber** `STRING` block number
- **from** `STRING` from address
- **hash** `STRING` transaction hash
- **transactionIndex** `STRING` transaction index

## `eth_getTransactionByBlockHashAndIndex`

Returns information about a transaction by block hash and transaction index position.

[Brief version](detailed-json-rpc.md#eth_getTransactionByBlockHashAndIndex)

**PARAMS**

1. **Block hash** `STRING` 32 byte hex value

1. **Transaction index** `STRING` hex encoded unsigned integer
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByBlockHashAndIndex",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "0x1"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByBlockHashAndIndex",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "0x1"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionByBlockHashAndIndex() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionByBlockHashAndIndex(
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "0x1"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionByBlockHashAndIndex();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "blockHash": "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "blockNumber": "0x77ed36",
    "transactionIndex": "0x1",
    "hash": "0x08f23a8d29dc0b23989b648f11fd89fad609c6694305b5d35e9b6d5fe1616d3a",
    "from": "0x22841539c4c3a3fa3c1355db7352adfb3a699ada",
    "to": null,
    "input": "0x608060405273b3cb14c326da065d8987e9ef4d771d758dad42a76000806101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555034801561006457600080fd5b50610196806100746000396000f3fe608060405234801561001057600080fd5b506004361061002b5760003560e01c80639e5faafc14610030575b600080fd5b61003861004e565b6040518082815260200191505060405180910390f35b60008067ffffffff0000ffff60c01b3360601b16905060005b611fff811161015a5760008054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16633370204e826201388001846040518363ffffffff1660e01b8152600401808277ffffffffffffffffffffffffffffffffffffffffffffffff19168152602001915050602060405180830381600088803b15801561010457600080fd5b5087f19350505050801561013957506040513d602081101561012557600080fd5b810190808051906020019092919050505060015b6101425761014d565b50809250505061015d565b8080600101915050610067565b50505b9056fea26469706673582212201082b38baaf4aa56ba1dbf14484c0ecabd8ba0cfb25a9b73905c51f3740d8bdb64736f6c634300060c0033",
    "nonce": "0x85",
    "value": "0x0",
    "gas": "0x282ac",
    "gasPrice": "0x9502f910",
    "maxPriorityFeePerGas": "0x9502f900",
    "maxFeePerGas": "0x9502f920",
    "accessList": [],
    "chainId": "0x5",
    "type": "0x2",
    "v": "0x0",
    "r": "0x1e4c8de7ea1e201d509144f8d081100db747267738c4f4b0e649cda6886f1e4c",
    "s": "0x6177915db9f2b5cd103bcf528a66cdad152f2394eabe42c0d357cd4c45600154"
  }
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Transaction information
Transaction information `OBJECT`

- **blockHash** `STRING` block hash
- **blockNumber** `STRING` block number
- **from** `STRING` from address
- **hash** `STRING` transaction hash
- **transactionIndex** `STRING` transaction index

## `eth_getTransactionByBlockNumberAndIndex`

Returns information about a transaction by block number and transaction index position.

[Brief version](detailed-json-rpc.md#eth_getTransactionByBlockNumberAndIndex)

**PARAMS**

1. **Block**

- `STRING` Block number

- `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

1. **Transaction index** `STRING` hex encoded unsigned integer
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByBlockNumberAndIndex",
  "params": ["latest", "0x1"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByBlockNumberAndIndex",
  "params": [
    "latest",
    "0x1"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionByBlockNumberAndIndex() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionByBlockNumberAndIndex(
    "latest",
    "0x1"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionByBlockNumberAndIndex();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "blockHash": "0x4f4facdbd8e6306776666f2c3f0a688d4fab66dc56c7bae7ecbdb32e96a45acc",
    "blockNumber": "0x77f0f6",
    "transactionIndex": "0x1",
    "hash": "0xd38bbdc5252f1676a0b83a6a652bac734c4db0fbc4631e487b7e6dbe32357cbb",
    "from": "0xde9c3edff91c41c55c9a3d76632b4a95871d987e",
    "to": "0xe08c99a3ccf28dad48c94a069f4492e55f1b818f",
    "input": "0x0f2123570000000000000000000000008efe26d6839108e831d3a37ca503ea4f136a8e7300000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000004563918244f40000000000000000000000000000000000000000000000000000000000000000002c6f6e6f6d7931367970786361677568326d787a716635796e6865677361656e737563687865396e6e73346d660000000000000000000000000000000000000000",
    "nonce": "0x2e",
    "value": "0x0",
    "gas": "0x17558",
    "gasPrice": "0x775676424",
    "maxPriorityFeePerGas": "0x775676424",
    "maxFeePerGas": "0x775676424",
    "accessList": [],
    "chainId": "0x5",
    "type": "0x2",
    "v": "0x1",
    "r": "0xad39fc7df3c65327f2c4134fa8690752e8805f7a9ed421013793629826aacdb7",
    "s": "0x18c3e481b39ba1cf027166e637d4980a53bbb253d23e51e5dd1ed69fc3991ba4"
  }
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Transaction information
Transaction information `OBJECT`

- **blockHash** `STRING` block hash
- **blockNumber** `STRING` block number
- **from** `STRING` from address
- **hash** `STRING` transaction hash
- **transactionIndex** `STRING` transaction index

## `eth_getTransactionReceipt`

Returns the receipt of a transaction by transaction hash.

[Brief version](detailed-json-rpc.md#eth_getTransactionReceipt)

**PARAMS**

1. **Transaction hash** (_optional_) `STRING` 32 byte hex value
   {% tabs %}
   {% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionReceipt",
  "params": [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionReceipt",
  "params": [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionReceipt() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionReceipt(
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionReceipt();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "type": "0x2",
    "status": "0x1",
    "cumulativeGasUsed": "0x65f9a6",
    "logsBloom": "0x02000008000000000000000000000000000000000000000000000004000000000000000000000000000000004000000000000000000000400000000000000000000000000000000000000000000000000000000000000000000000000000000040000000020000000000000000000800000000000000000000000000000000000000000000000000000000000000000000000080000000000000000000000008000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000008000000000",
    "logs": [
      {
        "address": "0xd9ded92319814d8f3587dfad7be72ca71e16697a",
        "topics": [
          "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
          "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
          "0x0000000000000000000000000000000000000000000000000000000000000000"
        ],
        "data": "0x",
        "blockNumber": "0x7787e4",
        "transactionHash": "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188",
        "transactionIndex": "0x24",
        "blockHash": "0xb39de02094847558d1b5b7be17899af87d4026419f063946d347aeb4b8f17b56",
        "logIndex": "0x55",
        "removed": false
      }
    ],
    "transactionHash": "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188",
    "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
    "to": "0xd9ded92319814d8f3587dfad7be72ca71e16697a",
    "contractAddress": null,
    "gasUsed": "0x19280",
    "effectiveGasPrice": "0x9a26693e",
    "blockHash": "0xb39de02094847558d1b5b7be17899af87d4026419f063946d347aeb4b8f17b56",
    "blockNumber": "0x7787e4",
    "transactionIndex": "0x24"
  }
}
```

{% endtab %}

{% endtabs %}

**RESULT**: Receipt Information
Receipt info `OBJECT`

- **transactionHash** `STRING` transaction hash
- **transactionIndex** `STRING` transaction index
- **blockHash** `STRING` block hash
- **blockNumber** `STRING` block number
- **from** `STRING` from
- **to** (_optional_) `STRING` to: Address of the receiver or null in a contract creation transaction.
- **cumulativeGasUsed** `STRING` cumulative gas used: The sum of gas used by this transaction and all preceding transactions in the same block.
- **gasUsed** `STRING` gas used: The amount of gas used for this specific transaction alone.
- **contractAddress** (_optional_) `ONEOF` of contract address: The contract address created, if the transaction was a contract creation, otherwise null.

  - `STRING` hex encoded address

  - `NULL`

- **logs** logs `ARRAY` of log `OBJECT`
  - **removed** (_optional_) `BOOLEAN` removed
  - **logIndex** (_optional_) `STRING` log index
  - **transactionIndex** (_optional_) `STRING` transaction index
  - **transactionHash** `STRING` transaction hash
  - **blockHash** (_optional_) `STRING` block hash
  - **blockNumber** (_optional_) `STRING` block number
  - **address** (_optional_) `STRING` address
  - **data** (_optional_) `STRING` data
  - **topics** (_optional_) topics `ARRAY` of `STRING` 32 hex encoded bytes
- **logsBloom** `STRING` logs bloom
- **root** (_optional_) `STRING` state root: The post-transaction state root. Only specified for transactions included before the Byzantium upgrade.
- **status** (_optional_) `STRING` status: Either 1 (success) or 0 (failure). Only specified for transactions included after the Byzantium upgrade.
- **effectiveGasPrice** `STRING` effective gas price: The actual value per gas deducted from the senders account. Before EIP-1559, this is equal to the transaction's gas price. After, it is equal to baseFeePerGas + min(maxFeePerGas - baseFeePerGas, maxPriorityFeePerGas).
