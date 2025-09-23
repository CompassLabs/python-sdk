# Token
(*token*)

## Overview

### Available Operations

* [token_price](#token_price) - Token Price
* [token_balance](#token_balance) - Token Balance
* [token_transfer](#token_transfer) - Transfer Tokens

## token_price

Retrieves the price of a token in USD using Chainlink's on-chain price feeds.

Chainlink is a decentralized oracle that aggregates price data from off-chain
sources. This ensures the price is tamper-resistant but the price might be stale
with the update frequency of the oracle.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_token_price" method="get" path="/v1/token/price" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.token.token_price(chain=models.V1TokenPriceChain.ETHEREUM, token="USDC")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         | Example                                                             |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `chain`                                                             | [models.V1TokenPriceChain](../../models/v1tokenpricechain.md)       | :heavy_check_mark:                                                  | N/A                                                                 |                                                                     |
| `token`                                                             | *str*                                                               | :heavy_check_mark:                                                  | The symbol or address of the token for which to get the price..     | USDC                                                                |
| `block`                                                             | *OptionalNullable[int]*                                             | :heavy_minus_sign:                                                  | Optional block number (defaults to latest).                         |                                                                     |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |                                                                     |

### Response

**[models.TokenPriceResponse](../../models/tokenpriceresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## token_balance

Returns the balance of a specific ERC20 token for a given user address.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_token_balance" method="get" path="/v1/token/balance" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.token.token_balance(chain=models.V1TokenBalanceChain.ARBITRUM, user="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", token="USDC")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                            | Type                                                                 | Required                                                             | Description                                                          | Example                                                              |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `chain`                                                              | [models.V1TokenBalanceChain](../../models/v1tokenbalancechain.md)    | :heavy_check_mark:                                                   | N/A                                                                  |                                                                      |
| `user`                                                               | *str*                                                                | :heavy_check_mark:                                                   | The user to get the token balance of.                                |                                                                      |
| `token`                                                              | *str*                                                                | :heavy_check_mark:                                                   | The symbol or address of the token for which the balance is checked. | USDC                                                                 |
| `retries`                                                            | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)     | :heavy_minus_sign:                                                   | Configuration to override the default retry behavior of the client.  |                                                                      |

### Response

**[models.TokenBalanceResponse](../../models/tokenbalanceresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## token_transfer

Sends native ETH or ERC20 tokens from the sender's address to another address.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_token_transfer" method="post" path="/v1/token/transfer" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.token.token_transfer(to="0x68b3465833fb72A70ecDF485E0e4C7bD8665Fc44", token="USDC", amount=1.5, chain=models.TokenTransferRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `to`                                                                                                                         | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The recipient of the tokens.                                                                                                 | 0x68b3465833fb72A70ecDF485E0e4C7bD8665Fc44                                                                                   |
| `token`                                                                                                                      | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the token to transfer.                                                                              | USDC                                                                                                                         |
| `amount`                                                                                                                     | [models.TokenTransferRequestAmount](../../models/tokentransferrequestamount.md)                                              | :heavy_check_mark:                                                                                                           | Amount of token to transfer                                                                                                  | 1.5                                                                                                                          |
| `chain`                                                                                                                      | [models.TokenTransferRequestChain](../../models/tokentransferrequestchain.md)                                                | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
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