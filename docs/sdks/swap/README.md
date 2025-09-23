# Swap
(*swap*)

## Overview

### Available Operations

* [swap_odos](#swap_odos) - Odos Swap

## swap_odos

Swap between two tokens using Odos Smart Order Routing.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `OdosRouter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_swap_odos" method="post" path="/v1/swap/odos" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.swap.swap_odos(token_in="0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48", token_out="0xdac17f958d2ee523a2206206994597c13d831ec7", amount=1.5, max_slippage_percent=0.5, chain=models.OdosSwapRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token_in`                                                                                                                   | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the token that is to be sold.                                                                       | 0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48                                                                                   |
| `token_out`                                                                                                                  | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the token that is to be bought.                                                                     | 0xdac17f958d2ee523a2206206994597c13d831ec7                                                                                   |
| `amount`                                                                                                                     | [models.OdosSwapRequestAmount](../../models/odosswaprequestamount.md)                                                        | :heavy_check_mark:                                                                                                           | The amount of token_in to be sold.                                                                                           | 1.5                                                                                                                          |
| `max_slippage_percent`                                                                                                       | *float*                                                                                                                      | :heavy_check_mark:                                                                                                           | The maximum slippage allowed in percent. e.g. `1` means `1%` slippage allowed.                                               | 0.5                                                                                                                          |
| `chain`                                                                                                                      | [models.OdosSwapRequestChain](../../models/odosswaprequestchain.md)                                                          | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.OdosTransactionResponse](../../models/odostransactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |