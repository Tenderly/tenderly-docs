# How to specify/change network chain\_id

`chain_id` is used as part of the transaction signing and in most cases is the same as the originating network, but what if you would like to change it?&#x20;

One reason can be to prevent the Fork environment from producing a signature valid on the actual network, in order to prevent a transaction replay attack:

```tsx
...

const body = {
  "network_id": "1", // network you wish to fork
	"block_number": "14386016",
	"chain_config": {
		"chain_id": "3" // chain_id used in the forked enviroment
	}
}

const resp = await axios.post(TENDERLY_FORK_API, body, opts);
```
