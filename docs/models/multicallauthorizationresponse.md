# MulticallAuthorizationResponse

Response model for multicall authorization.


## Fields

| Field                                         | Type                                          | Required                                      | Description                                   | Example                                       |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `nonce`                                       | *int*                                         | :heavy_check_mark:                            | A unique nonce value for this authorization   | 12345                                         |
| `address`                                     | *str*                                         | :heavy_check_mark:                            | The Ethereum address authorized for multicall |                                               |
| `chain_id`                                    | *int*                                         | :heavy_check_mark:                            | The chain ID for the blockchain network       | 1                                             |