# MorphoCheckUserPositionResponse


## Fields

| Field                                                      | Type                                                       | Required                                                   | Description                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `state`                                                    | [models.UserState](../models/userstate.md)                 | :heavy_check_mark:                                         | N/A                                                        |
| `vault_positions`                                          | List[[models.VaultPosition](../models/vaultposition.md)]   | :heavy_check_mark:                                         | A list of the user's vault positions.                      |
| `market_positions`                                         | List[[models.MarketPosition](../models/marketposition.md)] | :heavy_check_mark:                                         | A list of the user's market positions.                     |