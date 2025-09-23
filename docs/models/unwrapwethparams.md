# UnwrapWethParams

Parameters model for unwrapping WETH back to native ETH.


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          | Example                                                              |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `action_type`                                                        | *Optional[Literal["UNWRAP_WETH"]]*                                   | :heavy_minus_sign:                                                   | N/A                                                                  |                                                                      |
| `amount`                                                             | [models.UnwrapWethParamsAmount](../models/unwrapwethparamsamount.md) | :heavy_check_mark:                                                   | The amount of WETH to unwrap.                                        | 1.5                                                                  |