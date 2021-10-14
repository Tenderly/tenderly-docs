# Transaction Search API

## API Authentication

You can read more about API authentication here: [Authenticating with the Tenderly API](authenticating-with-the-tenderly-api.md).

## Transaction Search API

Endpoint:\
\
`https://api.tenderly.co/api/v1/account/{{username}}/project/{{project-slug}}/transactions?page=1&perPage=20`

Get parameters:

| Name             | Type      | Description                                                                                                                                                        | Mandatory Y/N |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- |
| page             | number    | the page of the transaction results                                                                                                                                | N             |
| perPage          | string    | number of txs to return                                                                                                                                            | N             |
| status           | string    | <p>true → returns successful txs <br><br>false → returns failed txs if nothing is passed returns all txsYY</p>                                                     | N             |
| txType           | string\[] | <p>internal → returns only internal txs <br><br>direct → returns only direct txs if nothing is passed returns all txs</p>                                          | N             |
| contractId\[]    | string    | <p>array of contract ids contract ids are in the format of: </p><p>eth:{{network_id}}:{{lowercase_addr}} <br><br>Note: the id must be the part of the projectN</p> | N             |
| functionSelector | string    | the function selector of the functionN                                                                                                                             | N             |
| after            | string    | ISO8601 date                                                                                                                                                       | N             |
| before           | string    | ISO8601 date                                                                                                                                                       | N             |
