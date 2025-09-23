# V1TokenPriceRequest


## Fields

| Field                                                           | Type                                                            | Required                                                        | Description                                                     | Example                                                         |
| --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| `chain`                                                         | [models.V1TokenPriceChain](../models/v1tokenpricechain.md)      | :heavy_check_mark:                                              | N/A                                                             |                                                                 |
| `block`                                                         | *OptionalNullable[int]*                                         | :heavy_minus_sign:                                              | Optional block number (defaults to latest).                     |                                                                 |
| `token`                                                         | *str*                                                           | :heavy_check_mark:                                              | The symbol or address of the token for which to get the price.. | USDC                                                            |