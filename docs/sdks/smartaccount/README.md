# SmartAccount
(*smart_account*)

## Overview

### Available Operations

* [smart_account_batched_user_operations](#smart_account_batched_user_operations) - Get Smart Account Batched User Operations

## smart_account_batched_user_operations

Generate a list of user operations for smart account batching.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_smart_account_batched_user_operations" method="post" path="/v1/smart_account/batched_user_operations" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.smart_account.smart_account_batched_user_operations(chain=models.BatchedUserOperationsRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", operations=[
        models.UserOperation(
            body=models.SetAllowanceParams(
                token="USDC",
                contract=models.SetAllowanceParamsContractEnum.UNISWAP_V3_ROUTER,
                amount="1000",
            ),
        ),
    ], estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                      | [models.BatchedUserOperationsRequestChain](../../models/batcheduseroperationsrequestchain.md)                                | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `operations`                                                                                                                 | List[[models.UserOperation](../../models/useroperation.md)]                                                                  | :heavy_check_mark:                                                                                                           | List of possible user operations                                                                                             | {<br/>"body": {<br/>"action_type": "SET_ALLOWANCE",<br/>"amount": "1000",<br/>"contract": "UniswapV3Router",<br/>"token": "USDC"<br/>}<br/>} |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.BatchedUserOperationsResponse](../../models/batcheduseroperationsresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |