# AaveSupportedTokenMetadata


## Fields

| Field                                        | Type                                         | Required                                     | Description                                  |
| -------------------------------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| `symbol`                                     | *str*                                        | :heavy_check_mark:                           | Token symbol (e.g., 'WETH', 'DAI').          |
| `address`                                    | *str*                                        | :heavy_check_mark:                           | Token contract address.                      |
| `supplying_enabled`                          | *bool*                                       | :heavy_check_mark:                           | Whether the token can be used as collateral. |
| `borrowing_enabled`                          | *bool*                                       | :heavy_check_mark:                           | Whether the token can be borrowed.           |