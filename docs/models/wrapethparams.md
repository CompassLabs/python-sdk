# WrapEthParams

Parameters model for wrapping ETH into WETH.


## Fields

| Field                                                          | Type                                                           | Required                                                       | Description                                                    | Example                                                        |
| -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| `action_type`                                                  | *Optional[Literal["WRAP_ETH"]]*                                | :heavy_minus_sign:                                             | N/A                                                            |                                                                |
| `amount`                                                       | [models.WrapEthParamsAmount](../models/wrapethparamsamount.md) | :heavy_check_mark:                                             | The amount of ETH to wrap.                                     | 1.5                                                            |