# TokenBalanceResponse

Response model for token balance information.


## Fields

| Field                                       | Type                                        | Required                                    | Description                                 | Example                                     |
| ------------------------------------------- | ------------------------------------------- | ------------------------------------------- | ------------------------------------------- | ------------------------------------------- |
| `amount`                                    | *str*                                       | :heavy_check_mark:                          | Amount of tokens a particular address holds | 1.5                                         |
| `decimals`                                  | *int*                                       | :heavy_check_mark:                          | Number of decimals of the token             | 18                                          |
| `token_symbol`                              | *str*                                       | :heavy_check_mark:                          | Symbol of the token                         |                                             |
| `token_address`                             | *str*                                       | :heavy_check_mark:                          | Address of the token                        | 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2  |