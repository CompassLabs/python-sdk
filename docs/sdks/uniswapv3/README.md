# UniswapV3
(*uniswap_v3*)

## Overview

### Available Operations

* [uniswap_quote_buy_exactly](#uniswap_quote_buy_exactly) - Get Quote - to Specified Amount
* [uniswap_quote_sell_exactly](#uniswap_quote_sell_exactly) - Get quote - From Specified Amount
* [uniswap_pool_price](#uniswap_pool_price) - Pool Price
* [uniswap_liquidity_provision_in_range](#uniswap_liquidity_provision_in_range) - Check if LP is Active.
* [uniswap_liquidity_provision_positions](#uniswap_liquidity_provision_positions) - List LP
* [uniswap_swap_buy_exactly](#uniswap_swap_buy_exactly) - Buy exact amount
* [uniswap_swap_sell_exactly](#uniswap_swap_sell_exactly) - Sell exact amount
* [uniswap_liquidity_provision_mint](#uniswap_liquidity_provision_mint) - Open a new LP position
* [uniswap_liquidity_provision_increase](#uniswap_liquidity_provision_increase) - Increase an LP position
* [uniswap_liquidity_provision_withdraw](#uniswap_liquidity_provision_withdraw) - Withdraw an LP position

## uniswap_quote_buy_exactly

This endpoint calculates the amount of input tokens required to purchase a
specified amount of output tokens from a Uniswap pool.

It also provides the resulting price after the transaction. The calculation takes
into account the current pool state and the specified fee tier.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_quote_buy_exactly" method="get" path="/v1/uniswap/quote/buy_exactly" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_quote_buy_exactly(chain=models.V1UniswapQuoteBuyExactlyChain.ARBITRUM, token_in="USDC", token_out="USDC", fee=models.V1UniswapQuoteBuyExactlyFeeEnum.ZERO_DOT_01, amount_out=9572.21)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                     | Type                                                                                          | Required                                                                                      | Description                                                                                   | Example                                                                                       |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `chain`                                                                                       | [models.V1UniswapQuoteBuyExactlyChain](../../models/v1uniswapquotebuyexactlychain.md)         | :heavy_check_mark:                                                                            | N/A                                                                                           |                                                                                               |
| `token_in`                                                                                    | *str*                                                                                         | :heavy_check_mark:                                                                            | The symbol or address of the token to swap from.                                              | USDC                                                                                          |
| `token_out`                                                                                   | *str*                                                                                         | :heavy_check_mark:                                                                            | The symbol or address of the token to swap to.                                                | USDC                                                                                          |
| `fee`                                                                                         | [models.V1UniswapQuoteBuyExactlyFeeEnum](../../models/v1uniswapquotebuyexactlyfeeenum.md)     | :heavy_check_mark:                                                                            | The fee to pay for the swap                                                                   |                                                                                               |
| `amount_out`                                                                                  | [models.V1UniswapQuoteBuyExactlyAmountOut](../../models/v1uniswapquotebuyexactlyamountout.md) | :heavy_check_mark:                                                                            | The amount of the token to swap to                                                            |                                                                                               |
| `retries`                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                              | :heavy_minus_sign:                                                                            | Configuration to override the default retry behavior of the client.                           |                                                                                               |

### Response

**[models.UniswapBuyQuoteInfoResponse](../../models/uniswapbuyquoteinforesponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_quote_sell_exactly

This endpoint calculates the amount of input tokens required to purchase a
specified amount of output tokens from a Uniswap pool.

It also provides the resulting price after the transaction. The calculation takes
into account the current pool state and the specified fee tier.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_quote_sell_exactly" method="get" path="/v1/uniswap/quote/sell_exactly" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_quote_sell_exactly(chain=models.V1UniswapQuoteSellExactlyChain.ARBITRUM, token_in="USDC", token_out="USDC", fee=models.V1UniswapQuoteSellExactlyFeeEnum.ZERO_DOT_01, amount_in=4736.09)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                     | Type                                                                                          | Required                                                                                      | Description                                                                                   | Example                                                                                       |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `chain`                                                                                       | [models.V1UniswapQuoteSellExactlyChain](../../models/v1uniswapquotesellexactlychain.md)       | :heavy_check_mark:                                                                            | N/A                                                                                           |                                                                                               |
| `token_in`                                                                                    | *str*                                                                                         | :heavy_check_mark:                                                                            | The symbol or address of the token to swap from.                                              | USDC                                                                                          |
| `token_out`                                                                                   | *str*                                                                                         | :heavy_check_mark:                                                                            | The symbol or address of the token to swap to.                                                | USDC                                                                                          |
| `fee`                                                                                         | [models.V1UniswapQuoteSellExactlyFeeEnum](../../models/v1uniswapquotesellexactlyfeeenum.md)   | :heavy_check_mark:                                                                            | The fee to pay for the swap                                                                   |                                                                                               |
| `amount_in`                                                                                   | [models.V1UniswapQuoteSellExactlyAmountIn](../../models/v1uniswapquotesellexactlyamountin.md) | :heavy_check_mark:                                                                            | The amount of the token to swap from                                                          |                                                                                               |
| `retries`                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                              | :heavy_minus_sign:                                                                            | Configuration to override the default retry behavior of the client.                           |                                                                                               |

### Response

**[models.UniswapSellQuoteInfoResponse](../../models/uniswapsellquoteinforesponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_pool_price

This endpoint calculates the price of a token in a Uniswap pool.

The price is calculated based on the current pool state and the specified fee tier.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_pool_price" method="get" path="/v1/uniswap/pool_price" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_pool_price(chain=models.V1UniswapPoolPriceChain.ARBITRUM, token_in="USDC", token_out="USDC", fee=models.V1UniswapPoolPriceFeeEnum.ZERO_DOT_01)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                     | Type                                                                          | Required                                                                      | Description                                                                   | Example                                                                       |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `chain`                                                                       | [models.V1UniswapPoolPriceChain](../../models/v1uniswappoolpricechain.md)     | :heavy_check_mark:                                                            | N/A                                                                           |                                                                               |
| `token_in`                                                                    | *str*                                                                         | :heavy_check_mark:                                                            | The symbol or address of a token in the pool                                  | USDC                                                                          |
| `token_out`                                                                   | *str*                                                                         | :heavy_check_mark:                                                            | The symbol or address of a token in the pool                                  | USDC                                                                          |
| `fee`                                                                         | [models.V1UniswapPoolPriceFeeEnum](../../models/v1uniswappoolpricefeeenum.md) | :heavy_check_mark:                                                            | The fee of the pool                                                           |                                                                               |
| `retries`                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)              | :heavy_minus_sign:                                                            | Configuration to override the default retry behavior of the client.           |                                                                               |

### Response

**[models.UniswapPoolPriceResponse](../../models/uniswappoolpriceresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_liquidity_provision_in_range

This endpoint allows users to check whether a specific liquidity provider ()
position is within the active tick range on the uniswap platform.

by providing the token id associated with the position, users can verify if the
position is currently within the tick range where trading occurs. this information
is essential for users to monitor the status of their lp positions and ensure that
they are actively participating in the trading activities within the liquidity pool
and earning trading fees.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_liquidity_provision_in_range" method="get" path="/v1/uniswap/liquidity_provision/in_range" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_liquidity_provision_in_range(chain=models.V1UniswapLiquidityProvisionInRangeChain.ARBITRUM, token_id=4318185)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                 | Type                                                                                                      | Required                                                                                                  | Description                                                                                               |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                   | [models.V1UniswapLiquidityProvisionInRangeChain](../../models/v1uniswapliquidityprovisioninrangechain.md) | :heavy_check_mark:                                                                                        | N/A                                                                                                       |
| `token_id`                                                                                                | *int*                                                                                                     | :heavy_check_mark:                                                                                        | Token ID of the NFT representing the liquidity provisioned position.                                      |
| `retries`                                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                          | :heavy_minus_sign:                                                                                        | Configuration to override the default retry behavior of the client.                                       |

### Response

**[models.UniswapCheckInRangeResponse](../../models/uniswapcheckinrangeresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_liquidity_provision_positions

This endpoint retrieves the number of Liquidity Provider (LP) positions
associated with a specific sender address on the Uniswap platform.

Users can query this endpoint to obtain detailed information about their LP
positions, including the total number of positions and relevant metadata. This
information is crucial for users to manage and analyze their liquidity provision
activities effectively.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_liquidity_provision_positions" method="get" path="/v1/uniswap/liquidity_provision/positions" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_liquidity_provision_positions(chain=models.V1UniswapLiquidityProvisionPositionsChain.ARBITRUM, user="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                     | Type                                                                                                          | Required                                                                                                      | Description                                                                                                   |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                       | [models.V1UniswapLiquidityProvisionPositionsChain](../../models/v1uniswapliquidityprovisionpositionschain.md) | :heavy_check_mark:                                                                                            | N/A                                                                                                           |
| `user`                                                                                                        | *Optional[str]*                                                                                               | :heavy_minus_sign:                                                                                            | The user to get positions for.                                                                                |
| `retries`                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                              | :heavy_minus_sign:                                                                                            | Configuration to override the default retry behavior of the client.                                           |

### Response

**[models.UniswapLPPositionsInfoResponse](../../models/uniswaplppositionsinforesponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_swap_buy_exactly

This endpoint allows users to trade a variable amount of one token to receive an
exact amount of another token using the Uniswap protocol.

The transaction is executed on the specified blockchain network, and the user must
provide the necessary transaction details, including the token to buy, the token to
pay with, and the exact amount to receive. If the token being paid with is ETH and
needs to be wrapped, the appropriate amount will be wrapped automatically.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `UniswapV3Router`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_swap_buy_exactly" method="post" path="/v1/uniswap/swap/buy_exactly" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_swap_buy_exactly(token_in="WETH", token_out="WETH", fee=models.FeeEnum.ONE_DOT_0, amount_out=1.5, max_slippage_percent=0.5, chain=models.UniswapBuyExactlyRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token_in`                                                                                                                   | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the token to swap from..                                                                            | WETH                                                                                                                         |
| `token_out`                                                                                                                  | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the token to swap to..                                                                              | WETH                                                                                                                         |
| `fee`                                                                                                                        | [models.FeeEnum](../../models/feeenum.md)                                                                                    | :heavy_check_mark:                                                                                                           | The transaction fee of a Uniswap pool in bips.<br/><br/>Uniswap supports 4 different fee levels.                             |                                                                                                                              |
| `amount_out`                                                                                                                 | [models.UniswapBuyExactlyRequestAmountOut](../../models/uniswapbuyexactlyrequestamountout.md)                                | :heavy_check_mark:                                                                                                           | The amount of 'token_out' to buy.                                                                                            | 1.5                                                                                                                          |
| `max_slippage_percent`                                                                                                       | *float*                                                                                                                      | :heavy_check_mark:                                                                                                           | The maximum slippage allowed in percent. e.g. `1` means `1 %` slippage allowed.                                              | 0.5                                                                                                                          |
| `chain`                                                                                                                      | [models.UniswapBuyExactlyRequestChain](../../models/uniswapbuyexactlyrequestchain.md)                                        | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.UniswapBuyExactlyTransactionResponse](../../models/uniswapbuyexactlytransactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_swap_sell_exactly

This endpoint allows users to trade a specific amount of one token into another
token using the Uniswap protocol.

The transaction is executed on the specified blockchain network, and the user must
provide the necessary transaction details, including the token to sell, the token to
receive, and the amount to sell. If the token being sold is ETH and needs to be
wrapped, the appropriate amount will be wrapped automatically.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `UniswapV3Router`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_swap_sell_exactly" method="post" path="/v1/uniswap/swap/sell_exactly" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_swap_sell_exactly(token_in="WETH", token_out="WETH", fee=models.FeeEnum.ONE_DOT_0, amount_in=1.5, max_slippage_percent=0.5, chain=models.UniswapSellExactlyRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token_in`                                                                                                                   | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the token to sell..                                                                                 | WETH                                                                                                                         |
| `token_out`                                                                                                                  | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the token to buy..                                                                                  | WETH                                                                                                                         |
| `fee`                                                                                                                        | [models.FeeEnum](../../models/feeenum.md)                                                                                    | :heavy_check_mark:                                                                                                           | The transaction fee of a Uniswap pool in bips.<br/><br/>Uniswap supports 4 different fee levels.                             |                                                                                                                              |
| `amount_in`                                                                                                                  | [models.UniswapSellExactlyRequestAmountIn](../../models/uniswapsellexactlyrequestamountin.md)                                | :heavy_check_mark:                                                                                                           | The amount of the `token_in` to sell                                                                                         | 1.5                                                                                                                          |
| `max_slippage_percent`                                                                                                       | *float*                                                                                                                      | :heavy_check_mark:                                                                                                           | The maximum slippage allowed in percent. e.g. `1` means `1 %` slippage allowed.                                              | 0.5                                                                                                                          |
| `chain`                                                                                                                      | [models.UniswapSellExactlyRequestChain](../../models/uniswapsellexactlyrequestchain.md)                                      | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.UniswapSellExactlyTransactionResponse](../../models/uniswapsellexactlytransactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_liquidity_provision_mint

This endpoint allows users to open a new Liquidity Provider (LP) position on the
Uniswap platform.

By providing the necessary parameters, users can initiate a minting process to
create a new LP token, which represents their stake in a specific liquidity pool.
This operation is essential for users looking to participate in liquidity provision,
enabling them to earn fees from trades that occur within the pool. The endpoint
requires details such as the token pair, amount, and any additional parameters
needed for the minting process.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `UniswapV3NFTPositionManager`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_liquidity_provision_mint" method="post" path="/v1/uniswap/liquidity_provision/mint" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_liquidity_provision_mint(token0="WETH", token1="WETH", fee=models.FeeEnum.ZERO_DOT_05, tick_lower=-1000, tick_upper=1000, amount0_desired="1.5", amount1_desired="1.7", amount0_min="1.4", amount1_min="1.6", chain=models.UniswapMintLiquidityProvisionRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", recipient="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                       | Type                                                                                                                            | Required                                                                                                                        | Description                                                                                                                     | Example                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `token0`                                                                                                                        | *str*                                                                                                                           | :heavy_check_mark:                                                                                                              | The symbol or address of the first token in the pair.                                                                           | WETH                                                                                                                            |
| `token1`                                                                                                                        | *str*                                                                                                                           | :heavy_check_mark:                                                                                                              | The symbol or address of the second token in the pair.                                                                          | WETH                                                                                                                            |
| `fee`                                                                                                                           | [models.FeeEnum](../../models/feeenum.md)                                                                                       | :heavy_check_mark:                                                                                                              | The transaction fee of a Uniswap pool in bips.<br/><br/>Uniswap supports 4 different fee levels.                                |                                                                                                                                 |
| `tick_lower`                                                                                                                    | *int*                                                                                                                           | :heavy_check_mark:                                                                                                              | The lower tick of the range to mint the position in                                                                             | -1000                                                                                                                           |
| `tick_upper`                                                                                                                    | *int*                                                                                                                           | :heavy_check_mark:                                                                                                              | The upper tick of the range to mint the position in                                                                             | 1000                                                                                                                            |
| `amount0_desired`                                                                                                               | [models.UniswapMintLiquidityProvisionRequestAmount0Desired](../../models/uniswapmintliquidityprovisionrequestamount0desired.md) | :heavy_check_mark:                                                                                                              | The desired amount of the first token to deposit                                                                                | 1.5                                                                                                                             |
| `amount1_desired`                                                                                                               | [models.UniswapMintLiquidityProvisionRequestAmount1Desired](../../models/uniswapmintliquidityprovisionrequestamount1desired.md) | :heavy_check_mark:                                                                                                              | The desired amount of the second token to deposit                                                                               | 1.7                                                                                                                             |
| `amount0_min`                                                                                                                   | [models.UniswapMintLiquidityProvisionRequestAmount0Min](../../models/uniswapmintliquidityprovisionrequestamount0min.md)         | :heavy_check_mark:                                                                                                              | The minimum amount of the first token to deposit                                                                                | 1.4                                                                                                                             |
| `amount1_min`                                                                                                                   | [models.UniswapMintLiquidityProvisionRequestAmount1Min](../../models/uniswapmintliquidityprovisionrequestamount1min.md)         | :heavy_check_mark:                                                                                                              | The minimum amount of the second token to deposit                                                                               | 1.6                                                                                                                             |
| `chain`                                                                                                                         | [models.UniswapMintLiquidityProvisionRequestChain](../../models/uniswapmintliquidityprovisionrequestchain.md)                   | :heavy_check_mark:                                                                                                              | N/A                                                                                                                             |                                                                                                                                 |
| `sender`                                                                                                                        | *str*                                                                                                                           | :heavy_check_mark:                                                                                                              | The address of the transaction sender.                                                                                          | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                      |
| `recipient`                                                                                                                     | *OptionalNullable[str]*                                                                                                         | :heavy_minus_sign:                                                                                                              | The address that will receive the LP tokens                                                                                     | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                      |
| `estimate_gas`                                                                                                                  | *Optional[bool]*                                                                                                                | :heavy_minus_sign:                                                                                                              | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.    |                                                                                                                                 |
| `retries`                                                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                | :heavy_minus_sign:                                                                                                              | Configuration to override the default retry behavior of the client.                                                             |                                                                                                                                 |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_liquidity_provision_increase

This endpoint allows users to increase their existing Liquidity Provider (LP)
positions on the Uniswap platform.

By providing the necessary parameters, users can add more liquidity to their current
positions, thereby increasing their stake in the liquidity pool. This operation is
beneficial for users who wish to enhance their potential earnings from trading fees
within the pool. The endpoint requires details such as the token pair, additional
amount to be added, and any other parameters necessary for the liquidity increase
process.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `AerodromeSlipstreamRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_liquidity_provision_increase" method="post" path="/v1/uniswap/liquidity_provision/increase" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_liquidity_provision_increase(token_id=991701, amount0_desired="1.5", amount1_desired="1.7", amount0_min="1.4", amount1_min="1.6", chain=models.UniswapIncreaseLiquidityProvisionRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                               | Type                                                                                                                                    | Required                                                                                                                                | Description                                                                                                                             | Example                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `token_id`                                                                                                                              | *int*                                                                                                                                   | :heavy_check_mark:                                                                                                                      | Token ID of the NFT representing the liquidity provisioned position.                                                                    |                                                                                                                                         |
| `amount0_desired`                                                                                                                       | [models.UniswapIncreaseLiquidityProvisionRequestAmount0Desired](../../models/uniswapincreaseliquidityprovisionrequestamount0desired.md) | :heavy_check_mark:                                                                                                                      | The desired amount of the first token to deposit                                                                                        | 1.5                                                                                                                                     |
| `amount1_desired`                                                                                                                       | [models.UniswapIncreaseLiquidityProvisionRequestAmount1Desired](../../models/uniswapincreaseliquidityprovisionrequestamount1desired.md) | :heavy_check_mark:                                                                                                                      | The desired amount of the second token to deposit                                                                                       | 1.7                                                                                                                                     |
| `amount0_min`                                                                                                                           | [models.UniswapIncreaseLiquidityProvisionRequestAmount0Min](../../models/uniswapincreaseliquidityprovisionrequestamount0min.md)         | :heavy_check_mark:                                                                                                                      | The minimum amount of the first token to deposit                                                                                        | 1.4                                                                                                                                     |
| `amount1_min`                                                                                                                           | [models.UniswapIncreaseLiquidityProvisionRequestAmount1Min](../../models/uniswapincreaseliquidityprovisionrequestamount1min.md)         | :heavy_check_mark:                                                                                                                      | The minimum amount of the second token to deposit                                                                                       | 1.6                                                                                                                                     |
| `chain`                                                                                                                                 | [models.UniswapIncreaseLiquidityProvisionRequestChain](../../models/uniswapincreaseliquidityprovisionrequestchain.md)                   | :heavy_check_mark:                                                                                                                      | N/A                                                                                                                                     |                                                                                                                                         |
| `sender`                                                                                                                                | *str*                                                                                                                                   | :heavy_check_mark:                                                                                                                      | The address of the transaction sender.                                                                                                  | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                              |
| `estimate_gas`                                                                                                                          | *Optional[bool]*                                                                                                                        | :heavy_minus_sign:                                                                                                                      | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.            |                                                                                                                                         |
| `retries`                                                                                                                               | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                        | :heavy_minus_sign:                                                                                                                      | Configuration to override the default retry behavior of the client.                                                                     |                                                                                                                                         |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## uniswap_liquidity_provision_withdraw

This endpoint allows users to withdraw their Liquidity Provider (LP) positions
from the Uniswap platform.

By specifying the necessary parameters, users can initiate the withdrawal process to
remove their stake from a specific liquidity pool. This operation is crucial for
users who wish to reclaim their assets or reallocate their liquidity to different
pools or investments. The endpoint requires details such as the token pair, the
amount to be withdrawn, and any additional parameters needed for the withdrawal
process. Users should ensure they meet any protocol requirements or conditions
before initiating a withdrawal to avoid potential issues or penalties.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `UniswapV3NFTPositionManager`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_uniswap_liquidity_provision_withdraw" method="post" path="/v1/uniswap/liquidity_provision/withdraw" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.uniswap_v3.uniswap_liquidity_provision_withdraw(token_id=821299, percentage_for_withdrawal="25", chain=models.UniswapWithdrawLiquidityProvisionRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                 | Type                                                                                                                                                      | Required                                                                                                                                                  | Description                                                                                                                                               | Example                                                                                                                                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `token_id`                                                                                                                                                | *int*                                                                                                                                                     | :heavy_check_mark:                                                                                                                                        | Token ID of the NFT representing the liquidity provisioned position.                                                                                      |                                                                                                                                                           |
| `percentage_for_withdrawal`                                                                                                                               | [models.UniswapWithdrawLiquidityProvisionRequestPercentageForWithdrawal](../../models/uniswapwithdrawliquidityprovisionrequestpercentageforwithdrawal.md) | :heavy_check_mark:                                                                                                                                        | How much liquidity to take out in percentage.                                                                                                             | 25                                                                                                                                                        |
| `chain`                                                                                                                                                   | [models.UniswapWithdrawLiquidityProvisionRequestChain](../../models/uniswapwithdrawliquidityprovisionrequestchain.md)                                     | :heavy_check_mark:                                                                                                                                        | N/A                                                                                                                                                       |                                                                                                                                                           |
| `sender`                                                                                                                                                  | *str*                                                                                                                                                     | :heavy_check_mark:                                                                                                                                        | The address of the transaction sender.                                                                                                                    | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                |
| `estimate_gas`                                                                                                                                            | *Optional[bool]*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                        | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                              |                                                                                                                                                           |
| `retries`                                                                                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                          | :heavy_minus_sign:                                                                                                                                        | Configuration to override the default retry behavior of the client.                                                                                       |                                                                                                                                                           |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |