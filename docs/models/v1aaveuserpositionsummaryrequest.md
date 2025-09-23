# V1AaveUserPositionSummaryRequest


## Fields

| Field                                                                                | Type                                                                                 | Required                                                                             | Description                                                                          |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `chain`                                                                              | [models.V1AaveUserPositionSummaryChain](../models/v1aaveuserpositionsummarychain.md) | :heavy_check_mark:                                                                   | N/A                                                                                  |
| `block`                                                                              | *OptionalNullable[int]*                                                              | :heavy_minus_sign:                                                                   | Optional block number (defaults to latest).                                          |
| `user`                                                                               | *str*                                                                                | :heavy_check_mark:                                                                   | The user to get position summary for.                                                |