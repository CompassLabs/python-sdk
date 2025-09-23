# V1AaveAvgRateRequest


## Fields

| Field                                                         | Type                                                          | Required                                                      | Description                                                   | Example                                                       |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `chain`                                                       | [models.V1AaveAvgRateChain](../models/v1aaveavgratechain.md)  | :heavy_check_mark:                                            | N/A                                                           |                                                               |
| `block`                                                       | *OptionalNullable[int]*                                       | :heavy_minus_sign:                                            | Optional block number (defaults to latest).                   |                                                               |
| `token`                                                       | *str*                                                         | :heavy_check_mark:                                            | The symbol or address of the token..                          | USDC                                                          |
| `days`                                                        | *int*                                                         | :heavy_check_mark:                                            | The number of days for which the average shall be calculated. |                                                               |