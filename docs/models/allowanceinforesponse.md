# AllowanceInfoResponse

Response model for token allowance information.


## Fields

| Field                                           | Type                                            | Required                                        | Description                                     | Example                                         |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `amount`                                        | *str*                                           | :heavy_check_mark:                              | Amount of tokens allowed to be spent by spender | 1.5                                             |
| `decimals`                                      | *int*                                           | :heavy_check_mark:                              | Number of decimals of the token                 | 18                                              |
| `token_symbol`                                  | *str*                                           | :heavy_check_mark:                              | Symbol of the token.                            | WETH                                            |
| `token_address`                                 | *str*                                           | :heavy_check_mark:                              | Address of the token                            | 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2      |
| `contract_address`                              | *str*                                           | :heavy_check_mark:                              | Address of the contract                         | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B      |