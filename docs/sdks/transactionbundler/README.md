# TransactionBundler
(*transaction_bundler*)

## Overview

### Available Operations

* [transaction_bundler_authorization](#transaction_bundler_authorization) - Enable Transaction Bundling
* [transaction_bundler_execute](#transaction_bundler_execute) - Construct Bundled Transaction
* [transaction_bundler_aave_loop](#transaction_bundler_aave_loop) - AAVE Leverage Long/Short

## transaction_bundler_authorization

Get authorization for bundling transactions.

Currently this is required for every transaction bundle to prevent replay attacks
and ensure transaction ordering when batching multiple actions into a single
transaction. The authorization includes a nonce and chain ID to guarantee
transaction uniqueness and proper network targeting.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_transaction_bundler_authorization" method="post" path="/v1/transaction_bundler/authorization" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.transaction_bundler.transaction_bundler_authorization(chain=models.MulticallAuthorizationRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                       | Type                                                                                            | Required                                                                                        | Description                                                                                     | Example                                                                                         |
| ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `chain`                                                                                         | [models.MulticallAuthorizationRequestChain](../../models/multicallauthorizationrequestchain.md) | :heavy_check_mark:                                                                              | N/A                                                                                             |                                                                                                 |
| `sender`                                                                                        | *str*                                                                                           | :heavy_check_mark:                                                                              | The Ethereum address to use for authorization                                                   | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                      |
| `retries`                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                | :heavy_minus_sign:                                                                              | Configuration to override the default retry behavior of the client.                             |                                                                                                 |

### Response

**[models.MulticallAuthorizationResponse](../../models/multicallauthorizationresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## transaction_bundler_execute

Bundle arbitrary transactions together into a single multicall transaction using
EIP-7702.

This endpoint allows bundling multiple contract calls into a single atomic
transaction, reducing gas costs and ensuring all operations succeed or fail
together. The transaction must be authorized using the /authorization endpoint to
prevent replay attacks.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_transaction_bundler_execute" method="post" path="/v1/transaction_bundler/execute" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.transaction_bundler.transaction_bundler_execute(chain=models.MulticallExecuteRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", actions=[
        models.UserOperation(
            body=models.SetAllowanceParams(
                token="WETH",
                contract=models.SetAllowanceParamsContractEnum.UNISWAP_V3_ROUTER,
                amount="1000",
            ),
        ),
    ], estimate_gas=True, signed_authorization={
        "nonce": 1000,
        "address": "0xcA11bde05977b3631167028862bE2a173976CA11",
        "chain_id": 42161,
        "r": "0x5f9f3f3226ac91bc01a72dd117141f6c6de1ed30d3af9f95c3423316dc21d615",
        "s": "0x78f7982ede9dabc53d7153974c5692fda8a21fc73bdafc42aaf135505e22817c",
        "y_parity": 0,
    })

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                        | Type                                                                                                                                                                                                                                                             | Required                                                                                                                                                                                                                                                         | Description                                                                                                                                                                                                                                                      | Example                                                                                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                                                                                                                                                          | [models.MulticallExecuteRequestChain](../../models/multicallexecuterequestchain.md)                                                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                                                               | N/A                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                  |
| `sender`                                                                                                                                                                                                                                                         | *str*                                                                                                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                                                               | The address of the transaction sender.                                                                                                                                                                                                                           | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                                                                                                                       |
| `actions`                                                                                                                                                                                                                                                        | List[[models.UserOperation](../../models/useroperation.md)]                                                                                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                                                               | List of possible actions for multicall                                                                                                                                                                                                                           | {<br/>"body": {<br/>"action_type": "SET_ALLOWANCE",<br/>"amount": "1000",<br/>"contract": "UniswapV3Router",<br/>"token": "WETH"<br/>}<br/>}                                                                                                                     |
| `estimate_gas`                                                                                                                                                                                                                                                   | *Optional[bool]*                                                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                               | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                                                                                                                     |                                                                                                                                                                                                                                                                  |
| `signed_authorization`                                                                                                                                                                                                                                           | [OptionalNullable[models.SignedAuthorization]](../../models/signedauthorization.md)                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                               | EIP-7702 authorization                                                                                                                                                                                                                                           | {<br/>"address": "0xcA11bde05977b3631167028862bE2a173976CA11",<br/>"chainId": 42161,<br/>"nonce": 1000,<br/>"r": "0x5f9f3f3226ac91bc01a72dd117141f6c6de1ed30d3af9f95c3423316dc21d615",<br/>"s": "0x78f7982ede9dabc53d7153974c5692fda8a21fc73bdafc42aaf135505e22817c",<br/>"yParity": 0<br/>} |
| `retries`                                                                                                                                                                                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                               | Configuration to override the default retry behavior of the client.                                                                                                                                                                                              |                                                                                                                                                                                                                                                                  |

### Response

**[models.BundlerTransactionResponse](../../models/bundlertransactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## transaction_bundler_aave_loop

Execute an Aave looping strategy that involves repeated supply and borrow
operations.

This endpoint creates a multicall transaction that performs a series of operations:
1. Approves and supplies initial token
2. For each loop:
    - Borrows another token
    - Swaps borrowed token back to supply token
    - Supplies the swapped tokens

The transaction must be authorized using the /authorization endpoint to prevent replay attacks.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_transaction_bundler_aave_loop" method="post" path="/v1/transaction_bundler/aave/loop" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.transaction_bundler.transaction_bundler_aave_loop(chain=models.AaveLoopRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", collateral_token="USDC", borrow_token="WETH", initial_collateral_amount="1000", multiplier="2.5", max_slippage_percent=2.5, loan_to_value=20.5, estimate_gas=True, signed_authorization={
        "nonce": 1000,
        "address": "0xcA11bde05977b3631167028862bE2a173976CA11",
        "chain_id": 42161,
        "r": "0x5f9f3f3226ac91bc01a72dd117141f6c6de1ed30d3af9f95c3423316dc21d615",
        "s": "0x78f7982ede9dabc53d7153974c5692fda8a21fc73bdafc42aaf135505e22817c",
        "y_parity": 0,
    }, is_account_abstraction=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                        | Type                                                                                                                                                                                                                                                             | Required                                                                                                                                                                                                                                                         | Description                                                                                                                                                                                                                                                      | Example                                                                                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                                                                                                                                                          | [models.AaveLoopRequestChain](../../models/aavelooprequestchain.md)                                                                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                                                               | N/A                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                  |
| `sender`                                                                                                                                                                                                                                                         | *str*                                                                                                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                                                               | The address of the transaction sender.                                                                                                                                                                                                                           | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                                                                                                                       |
| `collateral_token`                                                                                                                                                                                                                                               | *str*                                                                                                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                                                               | Symbol or address of token to supply to Aave..                                                                                                                                                                                                                   | USDC                                                                                                                                                                                                                                                             |
| `borrow_token`                                                                                                                                                                                                                                                   | *str*                                                                                                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                                                               | Symbol or address of token to borrow from Aave..                                                                                                                                                                                                                 | WETH                                                                                                                                                                                                                                                             |
| `initial_collateral_amount`                                                                                                                                                                                                                                      | [models.InitialCollateralAmount](../../models/initialcollateralamount.md)                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                               | Amount of collateral token to supply to Aave                                                                                                                                                                                                                     | 1000                                                                                                                                                                                                                                                             |
| `multiplier`                                                                                                                                                                                                                                                     | [models.Multiplier](../../models/multiplier.md)                                                                                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                                                               | Leverage multiplier. Total loop collateral will be calculated as `multiplier` x `initial_collateral_amount`                                                                                                                                                      | 2.5                                                                                                                                                                                                                                                              |
| `max_slippage_percent`                                                                                                                                                                                                                                           | [models.MaxSlippagePercent](../../models/maxslippagepercent.md)                                                                                                                                                                                                  | :heavy_check_mark:                                                                                                                                                                                                                                               | Maximum allowed slippage for token swaps in percentage                                                                                                                                                                                                           | 2.5                                                                                                                                                                                                                                                              |
| `loan_to_value`                                                                                                                                                                                                                                                  | [models.LoanToValue](../../models/loantovalue.md)                                                                                                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                                                               | Loan To Value percentage of the loop                                                                                                                                                                                                                             | 20.5                                                                                                                                                                                                                                                             |
| `estimate_gas`                                                                                                                                                                                                                                                   | *Optional[bool]*                                                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                               | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                                                                                                                     |                                                                                                                                                                                                                                                                  |
| `signed_authorization`                                                                                                                                                                                                                                           | [OptionalNullable[models.SignedAuthorization]](../../models/signedauthorization.md)                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                               | EIP-7702 authorization. Required when `is_account_abstraction` is False.                                                                                                                                                                                         | {<br/>"address": "0xcA11bde05977b3631167028862bE2a173976CA11",<br/>"chainId": 42161,<br/>"nonce": 1000,<br/>"r": "0x5f9f3f3226ac91bc01a72dd117141f6c6de1ed30d3af9f95c3423316dc21d615",<br/>"s": "0x78f7982ede9dabc53d7153974c5692fda8a21fc73bdafc42aaf135505e22817c",<br/>"yParity": 0<br/>} |
| `is_account_abstraction`                                                                                                                                                                                                                                         | *Optional[bool]*                                                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                               | Whether to use account abstraction for the transaction.                                                                                                                                                                                                          | true                                                                                                                                                                                                                                                             |
| `retries`                                                                                                                                                                                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                               | Configuration to override the default retry behavior of the client.                                                                                                                                                                                              |                                                                                                                                                                                                                                                                  |

### Response

**[models.ResponseV1TransactionBundlerAaveLoop](../../models/responsev1transactionbundleraaveloop.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |