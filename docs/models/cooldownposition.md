# CooldownPosition


## Fields

| Field                                                         | Type                                                          | Required                                                      | Description                                                   |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `amount_in_underlying_asset`                                  | *str*                                                         | :heavy_check_mark:                                            | The amount of USDe currently in a cooldown period.            |
| `cooldown_end`                                                | [models.CooldownEnd](../models/cooldownend.md)                | :heavy_check_mark:                                            | When the cooldown period ends. ISO 8601 format. UTC timezone. |
| `can_be_withdrawn`                                            | *bool*                                                        | :heavy_check_mark:                                            | Whether the USDe in cooldown can be withdrawn at this moment. |