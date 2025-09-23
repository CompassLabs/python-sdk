# CompassAPIBackendModelsPendleReadResponseMarketUserPosition


## Fields

| Field                                                            | Type                                                             | Required                                                         | Description                                                      |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| `claimable_yield`                                                | *str*                                                            | :heavy_check_mark:                                               | The amount of yield that can be claimed in the underlying token. |
| `sy_balance`                                                     | *str*                                                            | :heavy_check_mark:                                               | The amount of SY tokens the user currently holds.                |
| `pt_balance`                                                     | *str*                                                            | :heavy_check_mark:                                               | The amount of PT tokens the user currently holds.                |
| `yt_balance`                                                     | *str*                                                            | :heavy_check_mark:                                               | The amount of YT tokens the user currently holds.                |
| `lp_balance`                                                     | *str*                                                            | :heavy_check_mark:                                               | The amount of LP tokens the user currently holds.                |
| `underlying_token_balance`                                       | *str*                                                            | :heavy_check_mark:                                               | The amount of underlying tokens the user currently holds.        |
| `accounting_asset_balance`                                       | *OptionalNullable[str]*                                          | :heavy_minus_sign:                                               | The amount of accounting assets the user currently holds.        |