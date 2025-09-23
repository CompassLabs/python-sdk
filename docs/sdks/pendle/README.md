# Pendle
(*pendle*)

## Overview

### Available Operations

* [pendle_market](#pendle_market) - Get Market & User Position
* [pendle_positions](#pendle_positions) - List User's Market Positions
* [pendle_markets](#pendle_markets) - List Market Data
* [pendle_pt](#pendle_pt) - Trade Principal Token (PT)
* [pendle_yt](#pendle_yt) - Trade Yield Token (YT)
* [pendle_liquidity](#pendle_liquidity) - Manage Liquidity (LP)
* [pendle_redeem_yield](#pendle_redeem_yield) - Redeem Claimable Yield

## pendle_market

Get the market's implied APY, maturity date and the associated token data.

The user position is only included if 'user_address' parameter is included.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_pendle_market" method="get" path="/v1/pendle/market" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.pendle.pendle_market(chain=models.V1PendleMarketChain.ARBITRUM, market_address="0x46d62a8dede1bf2d0de04f2ed863245cbba5e538")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                       | Type                                                                                                                                            | Required                                                                                                                                        | Description                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                                         | [models.V1PendleMarketChain](../../models/v1pendlemarketchain.md)                                                                               | :heavy_check_mark:                                                                                                                              | N/A                                                                                                                                             |
| `market_address`                                                                                                                                | *str*                                                                                                                                           | :heavy_check_mark:                                                                                                                              | The market address of the desired position.                                                                                                     |
| `block`                                                                                                                                         | *OptionalNullable[int]*                                                                                                                         | :heavy_minus_sign:                                                                                                                              | Optional block number (defaults to latest).                                                                                                     |
| `user_address`                                                                                                                                  | *OptionalNullable[str]*                                                                                                                         | :heavy_minus_sign:                                                                                                                              | The user address of the desired market position. Only include if you would like the user position included in the response. Defaults to `None`. |
| `retries`                                                                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                | :heavy_minus_sign:                                                                                                                              | Configuration to override the default retry behavior of the client.                                                                             |

### Response

**[models.PendleGetMarketResponse](../../models/pendlegetmarketresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## pendle_positions

List the user's SY, PT, YT and LP positions for all markets on a given chain.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_pendle_positions" method="get" path="/v1/pendle/positions" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.pendle.pendle_positions(chain=models.V1PendlePositionsChain.ARBITRUM, user_address="0x68C314e30b543a35819e5625da563E6Da65D5dd4")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                               | Type                                                                    | Required                                                                | Description                                                             |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `chain`                                                                 | [models.V1PendlePositionsChain](../../models/v1pendlepositionschain.md) | :heavy_check_mark:                                                      | N/A                                                                     |
| `user_address`                                                          | *str*                                                                   | :heavy_check_mark:                                                      | The user address of the desired position.                               |
| `retries`                                                               | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)        | :heavy_minus_sign:                                                      | Configuration to override the default retry behavior of the client.     |

### Response

**[models.PendleListUserPositionsResponse](../../models/pendlelistuserpositionsresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## pendle_markets

Get a list of active markets.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_pendle_markets" method="get" path="/v1/pendle/markets" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.pendle.pendle_markets(chain=models.V1PendleMarketsChain.ARBITRUM)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `chain`                                                             | [models.V1PendleMarketsChain](../../models/v1pendlemarketschain.md) | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.PendleListMarketsResponse](../../models/pendlelistmarketsresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## pendle_pt

Trade market's Principal Token (PT) for fixed yield.

PT is traded with a token of the user's choice.

A sufficient allowance for the Pendle Router on the appropriate token contract must be set
beforehand. For `action` set to `BUY`, this is the `token` contract. For `action` set to `SELL`, this is the PT contract.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `PendleRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_pendle_pt" method="post" path="/v1/pendle/pt" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.pendle.pendle_pt(market_address="0x08a152834de126d2ef83d612ff36e4523fd0017f", action=models.PendleTradePtRequestAction.BUY, token="USDC", amount_in=1.5, max_slippage_percent=0.5, chain=models.PendleTradePtRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                        | Type                                                                                                                                                                             | Required                                                                                                                                                                         | Description                                                                                                                                                                      | Example                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `market_address`                                                                                                                                                                 | *str*                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                               | The address of the market identifying which Principal Token (PT) you would like to trade.                                                                                        | 0x08a152834de126d2ef83d612ff36e4523fd0017f                                                                                                                                       |
| `action`                                                                                                                                                                         | [models.PendleTradePtRequestAction](../../models/pendletradeptrequestaction.md)                                                                                                  | :heavy_check_mark:                                                                                                                                                               | Specifies the direction of the PT trade. Valid values are `BUY` (to buy PT) or `SELL` (to sell PT).                                                                              | BUY                                                                                                                                                                              |
| `token`                                                                                                                                                                          | *str*                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                               | TThe symbol or address of the token to trade PT with. For `action` set to `BUY`, this is the token to buy PT with. For `action` set to `SELL`, this is the token to sell PT for. | USDC                                                                                                                                                                             |
| `amount_in`                                                                                                                                                                      | [models.PendleTradePtRequestAmountIn](../../models/pendletradeptrequestamountin.md)                                                                                              | :heavy_check_mark:                                                                                                                                                               | For `action` set to `BUY`, this is the amount in of `token` to buy PT with. For `action` set to `SELL`, this is the amount in of PT to sell for `token`.                         | 1.5                                                                                                                                                                              |
| `max_slippage_percent`                                                                                                                                                           | *float*                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                               | The maximum slippage allowed in percent. e.g. `1` means `1%` slippage allowed.                                                                                                   | 0.5                                                                                                                                                                              |
| `chain`                                                                                                                                                                          | [models.PendleTradePtRequestChain](../../models/pendletradeptrequestchain.md)                                                                                                    | :heavy_check_mark:                                                                                                                                                               | N/A                                                                                                                                                                              |                                                                                                                                                                                  |
| `sender`                                                                                                                                                                         | *str*                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                               | The address of the transaction sender.                                                                                                                                           | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                                       |
| `estimate_gas`                                                                                                                                                                   | *Optional[bool]*                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                               | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                                     |                                                                                                                                                                                  |
| `retries`                                                                                                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                 | :heavy_minus_sign:                                                                                                                                                               | Configuration to override the default retry behavior of the client.                                                                                                              |                                                                                                                                                                                  |

### Response

**[models.PendleTxResponse](../../models/pendletxresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## pendle_yt

Trade Yield Token (YT) for variable yield.

YT is traded with a token of the user's choice.

A sufficient allowance for the Pendle Router on the appropriate token contract must be set
beforehand. For `action` set to `BUY`, this is the `token` contract. For `action` set to `SELL`, this is the YT contract.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `PendleRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_pendle_yt" method="post" path="/v1/pendle/yt" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.pendle.pendle_yt(market_address="0x08a152834de126d2ef83d612ff36e4523fd0017f", action=models.PendleTradeYtRequestAction.BUY, token="USDC", amount_in=1.5, max_slippage_percent=0.5, chain=models.PendleTradeYtRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                        | Type                                                                                                                                                                             | Required                                                                                                                                                                         | Description                                                                                                                                                                      | Example                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `market_address`                                                                                                                                                                 | *str*                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                               | The address of the market identifying which Yield Token (YT) you would like to trade.                                                                                            | 0x08a152834de126d2ef83d612ff36e4523fd0017f                                                                                                                                       |
| `action`                                                                                                                                                                         | [models.PendleTradeYtRequestAction](../../models/pendletradeytrequestaction.md)                                                                                                  | :heavy_check_mark:                                                                                                                                                               | Specifies the direction of the YT trade. Valid values are `BUY` (to buy YT) or `SELL` (to sell YT).                                                                              | BUY                                                                                                                                                                              |
| `token`                                                                                                                                                                          | *str*                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                               | TThe symbol or address of the token to trade YT with. For `action` set to `BUY`, this is the token to buy YT with. For `action` set to `SELL`, this is the token to sell YT for. | USDC                                                                                                                                                                             |
| `amount_in`                                                                                                                                                                      | [models.PendleTradeYtRequestAmountIn](../../models/pendletradeytrequestamountin.md)                                                                                              | :heavy_check_mark:                                                                                                                                                               | For `action` set to `BUY`, this is the amount in of `token` to buy YT with. For `action` set to `SELL`, this is the amount in of YT to sell for `token`.                         | 1.5                                                                                                                                                                              |
| `max_slippage_percent`                                                                                                                                                           | *float*                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                               | The maximum slippage allowed in percent. e.g. `1` means `1%` slippage allowed.                                                                                                   | 0.5                                                                                                                                                                              |
| `chain`                                                                                                                                                                          | [models.PendleTradeYtRequestChain](../../models/pendletradeytrequestchain.md)                                                                                                    | :heavy_check_mark:                                                                                                                                                               | N/A                                                                                                                                                                              |                                                                                                                                                                                  |
| `sender`                                                                                                                                                                         | *str*                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                               | The address of the transaction sender.                                                                                                                                           | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                                       |
| `estimate_gas`                                                                                                                                                                   | *Optional[bool]*                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                               | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                                     |                                                                                                                                                                                  |
| `retries`                                                                                                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                 | :heavy_minus_sign:                                                                                                                                                               | Configuration to override the default retry behavior of the client.                                                                                                              |                                                                                                                                                                                  |

### Response

**[models.PendleTxResponse](../../models/pendletxresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## pendle_liquidity

Manage liquidity in a Pendle Market.

Liquidity is supplied to or withdrawn from the market with a token of the user's choice.

Representation of the liquidity provided is in the form of market's Liquidity
Provider Token (LP) received by the user.

A sufficient allowance for the Pendle Router on the appropriate token contract must be set
beforehand. For `action` set to `SUPPLY`, this is the `token` contract. For `action` set to `WTIHDRAW`, this is the market contract (LP).
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `PendleRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_pendle_liquidity" method="post" path="/v1/pendle/liquidity" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.pendle.pendle_liquidity(market_address="0x08a152834de126d2ef83d612ff36e4523fd0017f", action=models.PendleManageLiquidityRequestAction.SUPPLY, token="USDC", amount_in=1.5, max_slippage_percent=0.5, chain=models.PendleManageLiquidityRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                  | Example                                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `market_address`                                                                                                                                                                                                             | *str*                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | The address identifying which Pendle Market you would like to add liquidity to.                                                                                                                                              | 0x08a152834de126d2ef83d612ff36e4523fd0017f                                                                                                                                                                                   |
| `action`                                                                                                                                                                                                                     | [models.PendleManageLiquidityRequestAction](../../models/pendlemanageliquidityrequestaction.md)                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                           | Specifies the direction of the liquidity operation for the Pendle market. Valid values are `SUPPLY` (to add liquidity) or `WITHDRAW` (to remove liquidity).                                                                  | SUPPLY                                                                                                                                                                                                                       |
| `token`                                                                                                                                                                                                                      | *str*                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | The symbol or address of the token to manage liquidity with. For `action` set to `SUPPLY`, this is the token to add as liquidity. For `action` set to `WITHDRAW`, this is the token to remove from liquidity.                | USDC                                                                                                                                                                                                                         |
| `amount_in`                                                                                                                                                                                                                  | [models.PendleManageLiquidityRequestAmountIn](../../models/pendlemanageliquidityrequestamountin.md)                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                           | For `action` set to `SUPPLY`, this is the amount in of `token` to add as liquidity in exchange for Liquidity Provider (LP) tokens. For `action` set to `WITHDRAW`, this is the amount in of LP tokens to redeem for `token`. | 1.5                                                                                                                                                                                                                          |
| `max_slippage_percent`                                                                                                                                                                                                       | *float*                                                                                                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                           | The maximum slippage allowed in percent. e.g. `1` means `1%` slippage allowed.                                                                                                                                               | 0.5                                                                                                                                                                                                                          |
| `chain`                                                                                                                                                                                                                      | [models.PendleManageLiquidityRequestChain](../../models/pendlemanageliquidityrequestchain.md)                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                           | N/A                                                                                                                                                                                                                          |                                                                                                                                                                                                                              |
| `sender`                                                                                                                                                                                                                     | *str*                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                           | The address of the transaction sender.                                                                                                                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                                                                                   |
| `estimate_gas`                                                                                                                                                                                                               | *Optional[bool]*                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                                                                                 |                                                                                                                                                                                                                              |
| `retries`                                                                                                                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                           | Configuration to override the default retry behavior of the client.                                                                                                                                                          |                                                                                                                                                                                                                              |

### Response

**[models.PendleTxResponse](../../models/pendletxresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## pendle_redeem_yield

Redeem claimable yield from the market's associated Yield Token (YT).
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `PendleRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_pendle_redeem_yield" method="post" path="/v1/pendle/redeem_yield" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.pendle.pendle_redeem_yield(market_address="0x08a152834de126d2ef83d612ff36e4523fd0017f", chain=models.PendleRedeemYieldRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `market_address`                                                                                                             | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the market identifying which Yield Token (YT) you would like to claim yield from.                             | 0x08a152834de126d2ef83d612ff36e4523fd0017f                                                                                   |
| `chain`                                                                                                                      | [models.PendleRedeemYieldRequestChain](../../models/pendleredeemyieldrequestchain.md)                                        | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |