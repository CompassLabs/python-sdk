# AerodromeSlipstream
(*aerodrome_slipstream*)

## Overview

### Available Operations

* [aerodrome_slipstream_liquidity_provision_positions](#aerodrome_slipstream_liquidity_provision_positions) - List LP Positions
* [aerodrome_slipstream_pool_price](#aerodrome_slipstream_pool_price) - Pool Price
* [aerodrome_slipstream_swap_sell_exactly](#aerodrome_slipstream_swap_sell_exactly) - Swap - from Specified Amount
* [aerodrome_slipstream_swap_buy_exactly](#aerodrome_slipstream_swap_buy_exactly) - Swap - into Specified Amount
* [aerodrome_slipstream_liquidity_provision_mint](#aerodrome_slipstream_liquidity_provision_mint) - Open a New LP Position
* [aerodrome_slipstream_liquidity_provision_increase](#aerodrome_slipstream_liquidity_provision_increase) - Increase an LP Position
* [aerodrome_slipstream_liquidity_provision_withdraw](#aerodrome_slipstream_liquidity_provision_withdraw) - Withdraw an LP Position

## aerodrome_slipstream_liquidity_provision_positions

Retrieve the total number of Liquidity Provider (LP) positions associated with a
specific sender.

This endpoint allows users to query and obtain detailed information about their LP
positions, including the number of active positions they hold. The response model,
AerodromeLPPositionsInfo, provides a structured representation of the LP positions
data, ensuring clarity and ease of use. This functionality is essential for users
managing their liquidity provision activities, enabling them to make informed
decisions based on their current positions.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aerodrome_slipstream_liquidity_provision_positions" method="get" path="/v1/aerodrome_slipstream/liquidity_provision/positions" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aerodrome_slipstream.aerodrome_slipstream_liquidity_provision_positions(chain=models.V1AerodromeSlipstreamLiquidityProvisionPositionsChain.BASE, user="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                             | Type                                                                                                                                  | Required                                                                                                                              | Description                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                               | [models.V1AerodromeSlipstreamLiquidityProvisionPositionsChain](../../models/v1aerodromeslipstreamliquidityprovisionpositionschain.md) | :heavy_check_mark:                                                                                                                    | N/A                                                                                                                                   |
| `user`                                                                                                                                | *Optional[str]*                                                                                                                       | :heavy_minus_sign:                                                                                                                    | The user to get positions for.                                                                                                        |
| `retries`                                                                                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                      | :heavy_minus_sign:                                                                                                                    | Configuration to override the default retry behavior of the client.                                                                   |

### Response

**[models.AerodromeLPPositionsResponse](../../models/aerodromelppositionsresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aerodrome_slipstream_pool_price

This endpoint retrieves the current price of a pool, indicating how many token0
you can purchase for 1 token1.

Note that this is an instantaneous price and may change during any trade. For a more
accurate representation of the trade ratios between the two assets, consider using
the quote endpoint.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aerodrome_slipstream_pool_price" method="get" path="/v1/aerodrome_slipstream/pool_price" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aerodrome_slipstream.aerodrome_slipstream_pool_price(chain=models.V1AerodromeSlipstreamPoolPriceChain.BASE, token_in="USDC", token_out="USDC", tick_spacing=100)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                         | Type                                                                                              | Required                                                                                          | Description                                                                                       | Example                                                                                           |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `chain`                                                                                           | [models.V1AerodromeSlipstreamPoolPriceChain](../../models/v1aerodromeslipstreampoolpricechain.md) | :heavy_check_mark:                                                                                | N/A                                                                                               |                                                                                                   |
| `token_in`                                                                                        | *str*                                                                                             | :heavy_check_mark:                                                                                | The symbol or address of a token in the pool.                                                     | USDC                                                                                              |
| `token_out`                                                                                       | *str*                                                                                             | :heavy_check_mark:                                                                                | The symbol or address of a token in the pool.                                                     | USDC                                                                                              |
| `tick_spacing`                                                                                    | *Optional[int]*                                                                                   | :heavy_minus_sign:                                                                                | The tick spacing of the pool                                                                      |                                                                                                   |
| `retries`                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                  | :heavy_minus_sign:                                                                                | Configuration to override the default retry behavior of the client.                               |                                                                                                   |

### Response

**[models.AerodromeSlipstreamPoolPriceResponse](../../models/aerodromeslipstreampoolpriceresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aerodrome_slipstream_swap_sell_exactly

This endpoint allows users to trade a specific amount of one token into another
token using the Aerodrome Slipstream protocol.

The transaction is executed by specifying the exact amount of the input token to be
sold, and the system calculates the amount of the output token that will be
received. The operation ensures that the trade is conducted within the constraints
of the current market conditions, taking into account the liquidity and price
impact. This endpoint is suitable for users who want to sell a precise quantity of a
token and are willing to accept the resulting amount of the other token.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AerodromeSlipstreamRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aerodrome_slipstream_swap_sell_exactly" method="post" path="/v1/aerodrome_slipstream/swap/sell_exactly" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aerodrome_slipstream.aerodrome_slipstream_swap_sell_exactly(token_in="WETH", token_out="WETH", tick_spacing=100, amount_in=1.5, chain=models.AerodromeSlipstreamSellExactlyRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", amount_out_minimum=1.4, estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                       | Type                                                                                                                                            | Required                                                                                                                                        | Description                                                                                                                                     | Example                                                                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `token_in`                                                                                                                                      | *str*                                                                                                                                           | :heavy_check_mark:                                                                                                                              | The symbol or address of the token to swap from.                                                                                                | WETH                                                                                                                                            |
| `token_out`                                                                                                                                     | *str*                                                                                                                                           | :heavy_check_mark:                                                                                                                              | The symbol or address of the token to swap to.                                                                                                  | WETH                                                                                                                                            |
| `tick_spacing`                                                                                                                                  | *int*                                                                                                                                           | :heavy_check_mark:                                                                                                                              | The tick spacing of the pool                                                                                                                    | 100                                                                                                                                             |
| `amount_in`                                                                                                                                     | [models.AerodromeSlipstreamSellExactlyRequestAmountIn](../../models/aerodromeslipstreamsellexactlyrequestamountin.md)                           | :heavy_check_mark:                                                                                                                              | The amount of the token to swap from                                                                                                            | 1.5                                                                                                                                             |
| `chain`                                                                                                                                         | [models.AerodromeSlipstreamSellExactlyRequestChain](../../models/aerodromeslipstreamsellexactlyrequestchain.md)                                 | :heavy_check_mark:                                                                                                                              | N/A                                                                                                                                             |                                                                                                                                                 |
| `sender`                                                                                                                                        | *str*                                                                                                                                           | :heavy_check_mark:                                                                                                                              | The address of the transaction sender.                                                                                                          | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                      |
| `amount_out_minimum`                                                                                                                            | [Optional[models.AerodromeSlipstreamSellExactlyRequestAmountOutMinimum]](../../models/aerodromeslipstreamsellexactlyrequestamountoutminimum.md) | :heavy_minus_sign:                                                                                                                              | The minimum amount of the token to swap to, defaults to 0                                                                                       | 1.4                                                                                                                                             |
| `estimate_gas`                                                                                                                                  | *Optional[bool]*                                                                                                                                | :heavy_minus_sign:                                                                                                                              | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                    |                                                                                                                                                 |
| `retries`                                                                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                | :heavy_minus_sign:                                                                                                                              | Configuration to override the default retry behavior of the client.                                                                             |                                                                                                                                                 |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aerodrome_slipstream_swap_buy_exactly

This endpoint facilitates the trading of tokens by allowing users to specify the
exact amount of the output token they wish to receive.

Utilizing the Aerodrome Slipstream protocol, the system calculates the necessary
amount of the input token required to achieve the desired output. This operation is
particularly useful for users who have a specific target amount of the output token
in mind and are willing to provide the corresponding input token amount. The
transaction is executed with consideration of current market conditions, including
liquidity and price impact, ensuring that the trade is completed efficiently and
effectively.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AerodromeSlipstreamRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aerodrome_slipstream_swap_buy_exactly" method="post" path="/v1/aerodrome_slipstream/swap/buy_exactly" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aerodrome_slipstream.aerodrome_slipstream_swap_buy_exactly(token_in="WETH", token_out="WETH", tick_spacing=100, amount_out=1.5, amount_in_maximum=1.6, chain=models.AerodromeSlipstreamBuyExactlyRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                         | Type                                                                                                                              | Required                                                                                                                          | Description                                                                                                                       | Example                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `token_in`                                                                                                                        | *str*                                                                                                                             | :heavy_check_mark:                                                                                                                | The symbol of the token to swap from.                                                                                             | WETH                                                                                                                              |
| `token_out`                                                                                                                       | *str*                                                                                                                             | :heavy_check_mark:                                                                                                                | The symbol of the token to swap to.                                                                                               | WETH                                                                                                                              |
| `tick_spacing`                                                                                                                    | *int*                                                                                                                             | :heavy_check_mark:                                                                                                                | The tick spacing of the pool                                                                                                      | 100                                                                                                                               |
| `amount_out`                                                                                                                      | [models.AerodromeSlipstreamBuyExactlyRequestAmountOut](../../models/aerodromeslipstreambuyexactlyrequestamountout.md)             | :heavy_check_mark:                                                                                                                | The amount of the token to swap to                                                                                                | 1.5                                                                                                                               |
| `amount_in_maximum`                                                                                                               | [models.AerodromeSlipstreamBuyExactlyRequestAmountInMaximum](../../models/aerodromeslipstreambuyexactlyrequestamountinmaximum.md) | :heavy_check_mark:                                                                                                                | The maximum amount of the token to swap from                                                                                      | 1.6                                                                                                                               |
| `chain`                                                                                                                           | [models.AerodromeSlipstreamBuyExactlyRequestChain](../../models/aerodromeslipstreambuyexactlyrequestchain.md)                     | :heavy_check_mark:                                                                                                                | N/A                                                                                                                               |                                                                                                                                   |
| `sender`                                                                                                                          | *str*                                                                                                                             | :heavy_check_mark:                                                                                                                | The address of the transaction sender.                                                                                            | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                        |
| `estimate_gas`                                                                                                                    | *Optional[bool]*                                                                                                                  | :heavy_minus_sign:                                                                                                                | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.      |                                                                                                                                   |
| `retries`                                                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                  | :heavy_minus_sign:                                                                                                                | Configuration to override the default retry behavior of the client.                                                               |                                                                                                                                   |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aerodrome_slipstream_liquidity_provision_mint

Initiate a new Liquidity Provider (LP) position by minting tokens.

This endpoint allows users to open a new LP position, enabling them to participate
in liquidity provision. The minting process involves creating a new position with
specified parameters, such as token amounts and pool details. The response will
confirm the successful creation of the LP position, providing users with the
necessary information to manage their newly minted position. This functionality is
crucial for users looking to expand their liquidity provision activities, offering
them the opportunity to engage in decentralized finance (DeFi) markets effectively.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AerodromeSlipstreamNonfungiblePositionManager`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aerodrome_slipstream_liquidity_provision_mint" method="post" path="/v1/aerodrome_slipstream/liquidity_provision/mint" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aerodrome_slipstream.aerodrome_slipstream_liquidity_provision_mint(token0="WETH", token1="USDC", tick_spacing=100, tick_lower=-1000, tick_upper=1000, amount0_desired="1.5", amount1_desired="1.7", amount0_min="1.4", amount1_min="1.6", chain=models.AerodromeSlipstreamMintLiquidityProvisionRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", recipient="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                               | Type                                                                                                                                                    | Required                                                                                                                                                | Description                                                                                                                                             | Example                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `token0`                                                                                                                                                | *str*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                      | The symbol or address of the first token in the pair.                                                                                                   | WETH                                                                                                                                                    |
| `token1`                                                                                                                                                | *str*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                      | The symbol or address of the second token in the pair.                                                                                                  | USDC                                                                                                                                                    |
| `tick_spacing`                                                                                                                                          | *int*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                      | The tick spacing of the pool                                                                                                                            | 100                                                                                                                                                     |
| `tick_lower`                                                                                                                                            | *int*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                      | The lower tick of the range to mint the position in                                                                                                     | -1000                                                                                                                                                   |
| `tick_upper`                                                                                                                                            | *int*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                      | The upper tick of the range to mint the position in                                                                                                     | 1000                                                                                                                                                    |
| `amount0_desired`                                                                                                                                       | [models.AerodromeSlipstreamMintLiquidityProvisionRequestAmount0Desired](../../models/aerodromeslipstreammintliquidityprovisionrequestamount0desired.md) | :heavy_check_mark:                                                                                                                                      | The desired amount of the first token to deposit                                                                                                        | 1.5                                                                                                                                                     |
| `amount1_desired`                                                                                                                                       | [models.AerodromeSlipstreamMintLiquidityProvisionRequestAmount1Desired](../../models/aerodromeslipstreammintliquidityprovisionrequestamount1desired.md) | :heavy_check_mark:                                                                                                                                      | The desired amount of the second token to deposit                                                                                                       | 1.7                                                                                                                                                     |
| `amount0_min`                                                                                                                                           | [models.AerodromeSlipstreamMintLiquidityProvisionRequestAmount0Min](../../models/aerodromeslipstreammintliquidityprovisionrequestamount0min.md)         | :heavy_check_mark:                                                                                                                                      | The minimum amount of the first token to deposit                                                                                                        | 1.4                                                                                                                                                     |
| `amount1_min`                                                                                                                                           | [models.AerodromeSlipstreamMintLiquidityProvisionRequestAmount1Min](../../models/aerodromeslipstreammintliquidityprovisionrequestamount1min.md)         | :heavy_check_mark:                                                                                                                                      | The minimum amount of the second token to deposit                                                                                                       | 1.6                                                                                                                                                     |
| `chain`                                                                                                                                                 | [models.AerodromeSlipstreamMintLiquidityProvisionRequestChain](../../models/aerodromeslipstreammintliquidityprovisionrequestchain.md)                   | :heavy_check_mark:                                                                                                                                      | N/A                                                                                                                                                     |                                                                                                                                                         |
| `sender`                                                                                                                                                | *str*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                      | The address of the transaction sender.                                                                                                                  | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                              |
| `recipient`                                                                                                                                             | *OptionalNullable[str]*                                                                                                                                 | :heavy_minus_sign:                                                                                                                                      | The address that will receive the LP tokens                                                                                                             | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                              |
| `estimate_gas`                                                                                                                                          | *Optional[bool]*                                                                                                                                        | :heavy_minus_sign:                                                                                                                                      | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                            |                                                                                                                                                         |
| `retries`                                                                                                                                               | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                        | :heavy_minus_sign:                                                                                                                                      | Configuration to override the default retry behavior of the client.                                                                                     |                                                                                                                                                         |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aerodrome_slipstream_liquidity_provision_increase

Increase the liquidity of an existing Liquidity Provider (LP) position.

This endpoint allows users to add more tokens to their current LP position,
enhancing their participation in liquidity provision. By increasing liquidity, users
can potentially earn more rewards and improve their position in the pool. The
process involves specifying additional token amounts and updating the pool details.
The response will confirm the successful increase of the LP position, providing
users with updated information about their enhanced position. This functionality is
vital for users aiming to optimize their liquidity provision strategy, enabling them
to adapt to market conditions and maximize their returns in decentralized finance
(DeFi) markets.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AerodromeSlipstreamRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aerodrome_slipstream_liquidity_provision_increase" method="post" path="/v1/aerodrome_slipstream/liquidity_provision/increase" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aerodrome_slipstream.aerodrome_slipstream_liquidity_provision_increase(token_id=312701, amount0_desired="1.5", amount1_desired="1.7", amount0_min="1.4", amount1_min="1.6", chain=models.AerodromeSlipstreamIncreaseLiquidityProvisionRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                       | Type                                                                                                                                                            | Required                                                                                                                                                        | Description                                                                                                                                                     | Example                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `token_id`                                                                                                                                                      | *int*                                                                                                                                                           | :heavy_check_mark:                                                                                                                                              | Token ID of the NFT representing the liquidity provisioned position.                                                                                            |                                                                                                                                                                 |
| `amount0_desired`                                                                                                                                               | [models.AerodromeSlipstreamIncreaseLiquidityProvisionRequestAmount0Desired](../../models/aerodromeslipstreamincreaseliquidityprovisionrequestamount0desired.md) | :heavy_check_mark:                                                                                                                                              | The desired amount of the first token to deposit                                                                                                                | 1.5                                                                                                                                                             |
| `amount1_desired`                                                                                                                                               | [models.AerodromeSlipstreamIncreaseLiquidityProvisionRequestAmount1Desired](../../models/aerodromeslipstreamincreaseliquidityprovisionrequestamount1desired.md) | :heavy_check_mark:                                                                                                                                              | The desired amount of the second token to deposit                                                                                                               | 1.7                                                                                                                                                             |
| `amount0_min`                                                                                                                                                   | [models.AerodromeSlipstreamIncreaseLiquidityProvisionRequestAmount0Min](../../models/aerodromeslipstreamincreaseliquidityprovisionrequestamount0min.md)         | :heavy_check_mark:                                                                                                                                              | The minimum amount of the first token to deposit                                                                                                                | 1.4                                                                                                                                                             |
| `amount1_min`                                                                                                                                                   | [models.AerodromeSlipstreamIncreaseLiquidityProvisionRequestAmount1Min](../../models/aerodromeslipstreamincreaseliquidityprovisionrequestamount1min.md)         | :heavy_check_mark:                                                                                                                                              | The minimum amount of the second token to deposit                                                                                                               | 1.6                                                                                                                                                             |
| `chain`                                                                                                                                                         | [models.AerodromeSlipstreamIncreaseLiquidityProvisionRequestChain](../../models/aerodromeslipstreamincreaseliquidityprovisionrequestchain.md)                   | :heavy_check_mark:                                                                                                                                              | N/A                                                                                                                                                             |                                                                                                                                                                 |
| `sender`                                                                                                                                                        | *str*                                                                                                                                                           | :heavy_check_mark:                                                                                                                                              | The address of the transaction sender.                                                                                                                          | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                      |
| `estimate_gas`                                                                                                                                                  | *Optional[bool]*                                                                                                                                                | :heavy_minus_sign:                                                                                                                                              | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                    |                                                                                                                                                                 |
| `retries`                                                                                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                | :heavy_minus_sign:                                                                                                                                              | Configuration to override the default retry behavior of the client.                                                                                             |                                                                                                                                                                 |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## aerodrome_slipstream_liquidity_provision_withdraw

Withdraw an existing Liquidity Provider (LP) position.

This endpoint allows users to remove their tokens from an LP position, effectively
closing their participation in the liquidity pool. The withdrawal process involves
specifying the LP position to be closed, and the response will confirm the
successful removal of liquidity, providing users with details about the withdrawn
tokens and any remaining balances. This functionality is essential for users who
wish to exit their liquidity provision activities, enabling them to reclaim their
assets and potentially reallocate them to other investment opportunities. The
endpoint ensures a smooth and secure withdrawal process, facilitating users'
strategic management of their decentralized finance (DeFi) portfolios.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AerodromeSlipstreamNonfungiblePositionManager`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_aerodrome_slipstream_liquidity_provision_withdraw" method="post" path="/v1/aerodrome_slipstream/liquidity_provision/withdraw" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aerodrome_slipstream.aerodrome_slipstream_liquidity_provision_withdraw(token_id=415732, percentage_for_withdrawal="25", chain=models.AerodromeSlipstreamWithdrawLiquidityProvisionRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                         | Type                                                                                                                                                                              | Required                                                                                                                                                                          | Description                                                                                                                                                                       | Example                                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `token_id`                                                                                                                                                                        | *int*                                                                                                                                                                             | :heavy_check_mark:                                                                                                                                                                | Token ID of the NFT representing the liquidity provisioned position.                                                                                                              |                                                                                                                                                                                   |
| `percentage_for_withdrawal`                                                                                                                                                       | [models.AerodromeSlipstreamWithdrawLiquidityProvisionRequestPercentageForWithdrawal](../../models/aerodromeslipstreamwithdrawliquidityprovisionrequestpercentageforwithdrawal.md) | :heavy_check_mark:                                                                                                                                                                | How much liquidity to take out in percentage.                                                                                                                                     | 25                                                                                                                                                                                |
| `chain`                                                                                                                                                                           | [models.AerodromeSlipstreamWithdrawLiquidityProvisionRequestChain](../../models/aerodromeslipstreamwithdrawliquidityprovisionrequestchain.md)                                     | :heavy_check_mark:                                                                                                                                                                | N/A                                                                                                                                                                               |                                                                                                                                                                                   |
| `sender`                                                                                                                                                                          | *str*                                                                                                                                                                             | :heavy_check_mark:                                                                                                                                                                | The address of the transaction sender.                                                                                                                                            | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                                        |
| `estimate_gas`                                                                                                                                                                    | *Optional[bool]*                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                                      |                                                                                                                                                                                   |
| `retries`                                                                                                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                | Configuration to override the default retry behavior of the client.                                                                                                               |                                                                                                                                                                                   |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |