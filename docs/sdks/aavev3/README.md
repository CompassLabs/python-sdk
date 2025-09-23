# AaveV3
(*aave_v3*)

## Overview

### Available Operations

* [aave_aave_supported_tokens](#aave_aave_supported_tokens) - Aave Supported Tokens
* [aave_rate](#aave_rate) - Interest Rates
* [aave_avg_rate](#aave_avg_rate) - Interest Rates: Time Average
* [aave_std_rate](#aave_std_rate) - Interest Rates: Standard Deviation
* [aave_reserve_overview](#aave_reserve_overview) - Reserve Overview
* [aave_token_price](#aave_token_price) - Token Prices
* [aave_liquidity_change](#aave_liquidity_change) - Liquidity Index
* [aave_user_position_summary](#aave_user_position_summary) - Positions - Total
* [aave_user_position_per_token](#aave_user_position_per_token) - Positions - per Token
* [aave_historical_transactions](#aave_historical_transactions) - Historical Transactions
* [aave_supply](#aave_supply) - Supply/Lend
* [aave_borrow](#aave_borrow) - Borrow
* [aave_repay](#aave_repay) - Repay Loans
* [aave_withdraw](#aave_withdraw) - Unstake

## aave_aave_supported_tokens

Returns the list of supported tokens on Aave for the specified network, along
with key metadata.

For each token, the response includes:
- The symbol and contract address.
- Whether the token is currently enabled for supplying (depositing).
- Whether it is enabled for borrowing.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_aave_supported_tokens" method="get" path="/v1/aave/aave_supported_tokens" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_aave_supported_tokens(chain=models.V1AaveAaveSupportedTokensChain.ARBITRUM)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                               | Type                                                                                    | Required                                                                                | Description                                                                             |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `chain`                                                                                 | [models.V1AaveAaveSupportedTokensChain](../../models/v1aaveaavesupportedtokenschain.md) | :heavy_check_mark:                                                                      | N/A                                                                                     |
| `block`                                                                                 | *OptionalNullable[int]*                                                                 | :heavy_minus_sign:                                                                      | Optional block number (defaults to latest).                                             |
| `retries`                                                                               | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                        | :heavy_minus_sign:                                                                      | Configuration to override the default retry behavior of the client.                     |

### Response

**[models.AaveSupportedTokensResponse](../../models/aavesupportedtokensresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_rate

Returns the latest APY and APR rates for a specified token on Aave, for both
deposits and loans.

**Annual percentage yield (APY)** is the yearly return/cost after continuous
compounding of the per-second rate stored on-chain. This value is the same value as
seen the on [app.aave.com](
https://app.aave.com/)
but more up-to-date as it is taken directly from the
blockchain every time this endpoint is called.

**Annual percentage rate (APR)** is the yearly simple interest rate (no
compounding).

For APY/APR on loans Aave offers both stable and fixed rates on certain tokens.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_rate" method="get" path="/v1/aave/rate" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_rate(chain=models.V1AaveRateChain.ARBITRUM, token="USDC")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                            | Type                                                                 | Required                                                             | Description                                                          | Example                                                              |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `chain`                                                              | [models.V1AaveRateChain](../../models/v1aaveratechain.md)            | :heavy_check_mark:                                                   | N/A                                                                  |                                                                      |
| `token`                                                              | *str*                                                                | :heavy_check_mark:                                                   | The symbol or address of the token to fetch the user's position on.. | USDC                                                                 |
| `block`                                                              | *OptionalNullable[int]*                                              | :heavy_minus_sign:                                                   | Optional block number (defaults to latest).                          |                                                                      |
| `retries`                                                            | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)     | :heavy_minus_sign:                                                   | Configuration to override the default retry behavior of the client.  |                                                                      |

### Response

**[models.AaveRateResponse](../../models/aaverateresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_avg_rate

Provides time-weighted averages of deposit and borrow rates for Aave reserves.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_avg_rate" method="get" path="/v1/aave/avg_rate" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_avg_rate(chain=models.V1AaveAvgRateChain.ETHEREUM, token="USDC", days=2)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         | Example                                                             |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `chain`                                                             | [models.V1AaveAvgRateChain](../../models/v1aaveavgratechain.md)     | :heavy_check_mark:                                                  | N/A                                                                 |                                                                     |
| `token`                                                             | *str*                                                               | :heavy_check_mark:                                                  | The symbol or address of the token..                                | USDC                                                                |
| `days`                                                              | *int*                                                               | :heavy_check_mark:                                                  | The number of days for which the average shall be calculated.       |                                                                     |
| `block`                                                             | *OptionalNullable[int]*                                             | :heavy_minus_sign:                                                  | Optional block number (defaults to latest).                         |                                                                     |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |                                                                     |

### Response

**[models.AaveAvgRateResponse](../../models/aaveavgrateresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_std_rate

Returns the historical standard deviation of lending and borrowing rates for Aave
reserves, illustrating market volatility.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_std_rate" method="get" path="/v1/aave/std_rate" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_std_rate(chain=models.V1AaveStdRateChain.ETHEREUM, token="USDC", days=7)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                | Type                                                                     | Required                                                                 | Description                                                              | Example                                                                  |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `chain`                                                                  | [models.V1AaveStdRateChain](../../models/v1aavestdratechain.md)          | :heavy_check_mark:                                                       | N/A                                                                      |                                                                          |
| `token`                                                                  | *str*                                                                    | :heavy_check_mark:                                                       | The symbol or address of the token..                                     | USDC                                                                     |
| `days`                                                                   | *int*                                                                    | :heavy_check_mark:                                                       | The number of days for which the standard deviation shall be calculated. |                                                                          |
| `block`                                                                  | *OptionalNullable[int]*                                                  | :heavy_minus_sign:                                                       | Optional block number (defaults to latest).                              |                                                                          |
| `retries`                                                                | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)         | :heavy_minus_sign:                                                       | Configuration to override the default retry behavior of the client.      |                                                                          |

### Response

**[models.AaveSTDRateResponse](../../models/aavestdrateresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_reserve_overview

Returns key metrics for Aave Reserves:
- Total Supplied (TVL) in USD
- Total Borrowed in USD
- Utilization Ratio

See below for more info:

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_reserve_overview" method="get" path="/v1/aave/reserve_overview" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_reserve_overview(chain=models.V1AaveReserveOverviewChain.ARBITRUM, token="USDC")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                       | Type                                                                            | Required                                                                        | Description                                                                     | Example                                                                         |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `chain`                                                                         | [models.V1AaveReserveOverviewChain](../../models/v1aavereserveoverviewchain.md) | :heavy_check_mark:                                                              | N/A                                                                             |                                                                                 |
| `token`                                                                         | *str*                                                                           | :heavy_check_mark:                                                              | The symbol or address of the asset..                                            | USDC                                                                            |
| `block`                                                                         | *OptionalNullable[int]*                                                         | :heavy_minus_sign:                                                              | Optional block number (defaults to latest).                                     |                                                                                 |
| `retries`                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                | :heavy_minus_sign:                                                              | Configuration to override the default retry behavior of the client.             |                                                                                 |

### Response

**[models.AaveReserveOverviewResponse](../../models/aavereserveoverviewresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_token_price

This endpoint retrieves the current price of a specified token in USD as
determined by the Aave protocol.

It utilizes the Aave V3 Oracle to fetch the token price, ensuring accurate and up-
to-date information. The request requires the token identifier and the blockchain
network (chain) on which the token resides. The response provides the token price in
a standardized format, converted from Wei to the base currency decimals defined by
Aave.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_token_price" method="get" path="/v1/aave/token_price" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_token_price(chain=models.V1AaveTokenPriceChain.ARBITRUM, token="USDC")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                             | Type                                                                  | Required                                                              | Description                                                           | Example                                                               |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `chain`                                                               | [models.V1AaveTokenPriceChain](../../models/v1aavetokenpricechain.md) | :heavy_check_mark:                                                    | N/A                                                                   |                                                                       |
| `token`                                                               | *str*                                                                 | :heavy_check_mark:                                                    | The symbol or address of the asset whose price you want..             | USDC                                                                  |
| `block`                                                               | *OptionalNullable[int]*                                               | :heavy_minus_sign:                                                    | Optional block number (defaults to latest).                           |                                                                       |
| `retries`                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)      | :heavy_minus_sign:                                                    | Configuration to override the default retry behavior of the client.   |                                                                       |

### Response

**[models.AaveTokenPriceResponse](../../models/aavetokenpriceresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_liquidity_change

This endpoint retrieves the change in the reserve liquidity index between two
provided blocks.

This is then converted to a percentage change. The liquidity index represents the
change in debt and interest accrual over each block. Aave does not store individual
user balances directly. Instead, it keeps a scaled balance and uses the liquidity
index to compute real balances dynamically. If a user was to have deposited tokens
at the start block, a positive liquidity index change will represent accrued
interest and a profit. If tokens were borrowed at the start block, this debt will
increase, compound on itself and represent large debt. The reverse in both cases is
true if the liquidity index is negative.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_liquidity_change" method="get" path="/v1/aave/liquidity/change" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_liquidity_change(chain=models.V1AaveLiquidityChangeChain.ARBITRUM, token="USDC", start_block=0, end_block=319407231)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                       | Type                                                                            | Required                                                                        | Description                                                                     | Example                                                                         |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `chain`                                                                         | [models.V1AaveLiquidityChangeChain](../../models/v1aaveliquiditychangechain.md) | :heavy_check_mark:                                                              | N/A                                                                             |                                                                                 |
| `token`                                                                         | *str*                                                                           | :heavy_check_mark:                                                              | The symbol or address of the asset to get liquidity change for..                | USDC                                                                            |
| `start_block`                                                                   | *int*                                                                           | :heavy_check_mark:                                                              | The start block to calculate liquidity change from.                             |                                                                                 |
| `end_block`                                                                     | *int*                                                                           | :heavy_check_mark:                                                              | The end block to calculate liquidity change to.                                 |                                                                                 |
| `retries`                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                | :heavy_minus_sign:                                                              | Configuration to override the default retry behavior of the client.             |                                                                                 |

### Response

**[models.AaveLiquidityChangeResponse](../../models/aaveliquiditychangeresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_user_position_summary

This endpoint retrieves a comprehensive summary of a user's position on the AAVE
platform.

It provides key financial metrics including the total collateral deposited, total
debt accrued, available borrowing capacity, liquidation threshold, maximum loan-to-
value ratio, and the health factor of the user's account. These metrics are
calculated by aggregating data across all open positions held by the user, offering
a holistic view of their financial standing within the AAVE ecosystem.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_user_position_summary" method="get" path="/v1/aave/user_position_summary" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_user_position_summary(chain=models.V1AaveUserPositionSummaryChain.BASE, user="0x3254f3b1918637ba924e3F18968Cb74219974b63")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                               | Type                                                                                    | Required                                                                                | Description                                                                             |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `chain`                                                                                 | [models.V1AaveUserPositionSummaryChain](../../models/v1aaveuserpositionsummarychain.md) | :heavy_check_mark:                                                                      | N/A                                                                                     |
| `user`                                                                                  | *str*                                                                                   | :heavy_check_mark:                                                                      | The user to get position summary for.                                                   |
| `block`                                                                                 | *OptionalNullable[int]*                                                                 | :heavy_minus_sign:                                                                      | Optional block number (defaults to latest).                                             |
| `retries`                                                                               | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                        | :heavy_minus_sign:                                                                      | Configuration to override the default retry behavior of the client.                     |

### Response

**[models.AaveUserPositionSummaryResponse](../../models/aaveuserpositionsummaryresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_user_position_per_token

This endpoint retrieves the user's position for a specific token on the AAVE
platform.

It provides key financial metrics including the current aToken balance, current
stable debt, current variable debt, principal stable debt, principal variable debt,
stable borrow rate, stable borrow rate for new loans, variable borrow rate, and
liquidity rate. These metrics are calculated by aggregating data across all open
positions held by the user for the specified token, offering a detailed view of
their financial standing within the AAVE ecosystem.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_user_position_per_token" method="get" path="/v1/aave/user_position_per_token" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_user_position_per_token(chain=models.V1AaveUserPositionPerTokenChain.BASE, user="0x3254f3b1918637ba924e3F18968Cb74219974b63", token="USDC")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                 | Type                                                                                      | Required                                                                                  | Description                                                                               | Example                                                                                   |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `chain`                                                                                   | [models.V1AaveUserPositionPerTokenChain](../../models/v1aaveuserpositionpertokenchain.md) | :heavy_check_mark:                                                                        | N/A                                                                                       |                                                                                           |
| `user`                                                                                    | *str*                                                                                     | :heavy_check_mark:                                                                        | The user to fetch the token-specific position of.                                         |                                                                                           |
| `token`                                                                                   | *str*                                                                                     | :heavy_check_mark:                                                                        | The symbol or address of the asset to fetch the user's position on..                      | USDC                                                                                      |
| `block`                                                                                   | *OptionalNullable[int]*                                                                   | :heavy_minus_sign:                                                                        | Optional block number (defaults to latest).                                               |                                                                                           |
| `retries`                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                          | :heavy_minus_sign:                                                                        | Configuration to override the default retry behavior of the client.                       |                                                                                           |

### Response

**[models.AaveUserPositionPerTokenResponse](../../models/aaveuserpositionpertokenresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_historical_transactions

This endpoint retrieves historical transactions for a user on the AAVE platform.

It returns a list of transactions including deposits, withdrawals, borrows, and
repayments. Each transaction includes details such as the token, amount, timestamp,
and transaction type. This provides a comprehensive view of the user's historical
activity within the AAVE protocol.

⚠️ Data comes from the official Aave subgraph (
https://github.com/aave/protocol-subgraphs)
and thus this particular endpoint may be less reliable than our other endpoints. ⚠️

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_historical_transactions" method="get" path="/v1/aave/historical_transactions" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_historical_transactions(chain=models.V1AaveHistoricalTransactionsChain.BASE, user_address="0x3254f3b1918637ba924e3F18968Cb74219974b63", offset=0, limit=100)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                     | Type                                                                                          | Required                                                                                      | Description                                                                                   |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `chain`                                                                                       | [models.V1AaveHistoricalTransactionsChain](../../models/v1aavehistoricaltransactionschain.md) | :heavy_check_mark:                                                                            | N/A                                                                                           |
| `user_address`                                                                                | *str*                                                                                         | :heavy_check_mark:                                                                            | The address of the user to get historical transactions for.                                   |
| `offset`                                                                                      | *Optional[int]*                                                                               | :heavy_minus_sign:                                                                            | The offset of the first item to return.                                                       |
| `limit`                                                                                       | *Optional[int]*                                                                               | :heavy_minus_sign:                                                                            | The number of items to return.                                                                |
| `retries`                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                              | :heavy_minus_sign:                                                                            | Configuration to override the default retry behavior of the client.                           |

### Response

**[models.AaveHistoricalTransactionsResponse](../../models/aavehistoricaltransactionsresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_supply

By supplying assets, users can earn interest on their deposits.

The supplied collateral can be used as a basis for borrowing other assets, allowing
users to leverage their positions. In combination with a trading protocol, this can
create leverage.

Overall, this endpoint is a critical component for users looking to maximize their
asset utility within the AAVEv3 ecosystem, providing both earning potential and
borrowing flexibility.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AaveV3Pool`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_supply" method="post" path="/v1/aave/supply" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_supply(token="WETH", amount=1.5, chain=models.AaveSupplyRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token`                                                                                                                      | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the underlying asset to supply as collateral. You can borrow against it..                           | WETH                                                                                                                         |
| `amount`                                                                                                                     | [models.AaveSupplyRequestAmount](../../models/aavesupplyrequestamount.md)                                                    | :heavy_check_mark:                                                                                                           | The amount of the asset to supply                                                                                            | 1.5                                                                                                                          |
| `chain`                                                                                                                      | [models.AaveSupplyRequestChain](../../models/aavesupplyrequestchain.md)                                                      | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `on_behalf_of`                                                                                                               | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address on behalf of whom the supply is made. Defaults to the transaction sender.                                        |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_borrow

You will pay interest for your borrows.

Price changes in the assets may lead to some or all of your collateral being
liquidated, if the borrow position becomes unhealthy.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AaveV3Pool`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_borrow" method="post" path="/v1/aave/borrow" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_borrow(token="WETH", amount=150.5, interest_rate_mode=models.InterestRateMode.STABLE, chain=models.AaveBorrowRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token`                                                                                                                      | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the underlying asset to borrow..                                                                    | WETH                                                                                                                         |
| `amount`                                                                                                                     | [models.AaveBorrowRequestAmount](../../models/aaveborrowrequestamount.md)                                                    | :heavy_check_mark:                                                                                                           | The amount of the asset to borrow                                                                                            | 150.5                                                                                                                        |
| `interest_rate_mode`                                                                                                         | [models.InterestRateMode](../../models/interestratemode.md)                                                                  | :heavy_check_mark:                                                                                                           | On AAVE there are 2 different interest modes.<br/><br/>A stable (but typically higher rate), or a variable rate.             |                                                                                                                              |
| `chain`                                                                                                                      | [models.AaveBorrowRequestChain](../../models/aaveborrowrequestchain.md)                                                      | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `on_behalf_of`                                                                                                               | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address on behalf of whom the supply is made                                                                             |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_repay

This endpoint allows users to repay a portion or the entirety of their borrowed
tokens on the Aave platform.

By repaying borrowed amounts, users can improve their health factor, which is a
measure of the safety of their loan position. A higher health factor reduces the
risk of liquidation, ensuring a more secure borrowing experience. The endpoint
requires specifying the chain and the details of the repayment transaction,
including the amount and the asset to be repaid.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AaveV3Pool`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_repay" method="post" path="/v1/aave/repay" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_repay(token="WETH", amount=150.5, interest_rate_mode=models.InterestRateMode.STABLE, chain=models.AaveRepayRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token`                                                                                                                      | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol of the underlying asset to repay..                                                                                | WETH                                                                                                                         |
| `amount`                                                                                                                     | [models.AaveRepayRequestAmount](../../models/aaverepayrequestamount.md)                                                      | :heavy_check_mark:                                                                                                           | The amount of the asset to repay                                                                                             | 150.5                                                                                                                        |
| `interest_rate_mode`                                                                                                         | [models.InterestRateMode](../../models/interestratemode.md)                                                                  | :heavy_check_mark:                                                                                                           | On AAVE there are 2 different interest modes.<br/><br/>A stable (but typically higher rate), or a variable rate.             |                                                                                                                              |
| `chain`                                                                                                                      | [models.AaveRepayRequestChain](../../models/aaverepayrequestchain.md)                                                        | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `on_behalf_of`                                                                                                               | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address on behalf of whom the supply is made                                                                             |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aave_withdraw

This endpoint facilitates the withdrawal of collateral from the Aave protocol.

Users can withdraw a portion or all of their collateral, which may increase the risk
of liquidation if there are outstanding borrows. The withdrawal process also
includes the collection of any interest earned on the collateral. It is important
for users to carefully consider their outstanding debts and the potential impact on
their liquidation threshold before proceeding with a withdrawal. This endpoint is
designed to provide a seamless and efficient way to manage your collateral within
the Aave ecosystem.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AaveV3Pool`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aave_withdraw" method="post" path="/v1/aave/withdraw" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_withdraw(token="WETH", amount=1.5, recipient="0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2", chain=models.AaveWithdrawRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token`                                                                                                                      | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol of the underlying asset to withdraw..                                                                             | WETH                                                                                                                         |
| `amount`                                                                                                                     | [models.AaveWithdrawRequestAmount](../../models/aavewithdrawrequestamount.md)                                                | :heavy_check_mark:                                                                                                           | The amount of the asset to withdraw                                                                                          | 1.5                                                                                                                          |
| `recipient`                                                                                                                  | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the recipient of the withdrawn funds.                                                                         | 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2                                                                                   |
| `chain`                                                                                                                      | [models.AaveWithdrawRequestChain](../../models/aavewithdrawrequestchain.md)                                                  | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
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