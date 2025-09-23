# Ethena
(*ethena*)

## Overview

### Available Operations

* [ethena_vault](#ethena_vault) - Get Vault & User Position
* [ethena_deposit](#ethena_deposit) - Deposit USDe
* [ethena_request](#ethena_request) - Request to Withdraw USDe
* [ethena_unstake](#ethena_unstake) - Unstake USDe

## ethena_vault

Get data & user Position for the Ethena vault on Ethereum.

Vault address: 0x9d39a5de30e57443bff2a8307a4256c8797a3497

The user position is only included in the response if 'user_address' parameter is included in the request.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_ethena_vault" method="get" path="/v1/ethena/vault" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.ethena.ethena_vault(chain=models.V1EthenaVaultChain.ETHEREUM)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                      | Type                                                                                                                                           | Required                                                                                                                                       | Description                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                                        | [models.V1EthenaVaultChain](../../models/v1ethenavaultchain.md)                                                                                | :heavy_check_mark:                                                                                                                             | N/A                                                                                                                                            |
| `block`                                                                                                                                        | *OptionalNullable[int]*                                                                                                                        | :heavy_minus_sign:                                                                                                                             | Optional block number (defaults to latest).                                                                                                    |
| `user_address`                                                                                                                                 | *OptionalNullable[str]*                                                                                                                        | :heavy_minus_sign:                                                                                                                             | The user address of the desired vault position. Only include if you would like the user position included in the response. Defaults to `None`. |
| `retries`                                                                                                                                      | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                               | :heavy_minus_sign:                                                                                                                             | Configuration to override the default retry behavior of the client.                                                                            |

### Response

**[models.EthenaGetVaultResponse](../../models/ethenagetvaultresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## ethena_deposit

Deposit USDe into a Ethena's Vault to earn passive yield.

The shares of a deposit are respresented as sUSDe.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `EthenaVault`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_ethena_deposit" method="post" path="/v1/ethena/deposit" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.ethena.ethena_deposit(amount=1.5, chain=models.EthenaDepositRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                      | Type                                                                                                                                                           | Required                                                                                                                                                       | Description                                                                                                                                                    | Example                                                                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                                                       | [models.EthenaDepositRequestAmount](../../models/ethenadepositrequestamount.md)                                                                                | :heavy_check_mark:                                                                                                                                             | The amount of USDe to deposit into Ethena's vault.                                                                                                             | 1.5                                                                                                                                                            |
| `chain`                                                                                                                                                        | [models.EthenaDepositRequestChain](../../models/ethenadepositrequestchain.md)                                                                                  | :heavy_check_mark:                                                                                                                                             | N/A                                                                                                                                                            |                                                                                                                                                                |
| `sender`                                                                                                                                                       | *str*                                                                                                                                                          | :heavy_check_mark:                                                                                                                                             | The address of the transaction sender.                                                                                                                         | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                     |
| `receiver`                                                                                                                                                     | *OptionalNullable[str]*                                                                                                                                        | :heavy_minus_sign:                                                                                                                                             | The address which will receive the shares (sUSDe) from Ethena's vault representing their proportional ownership of the vault's assets. Defaults to the sender. |                                                                                                                                                                |
| `estimate_gas`                                                                                                                                                 | *Optional[bool]*                                                                                                                                               | :heavy_minus_sign:                                                                                                                                             | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                   |                                                                                                                                                                |
| `retries`                                                                                                                                                      | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                               | :heavy_minus_sign:                                                                                                                                             | Configuration to override the default retry behavior of the client.                                                                                            |                                                                                                                                                                |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## ethena_request

Request to withdraw deposited USDe from Ethena's vault.

The Ethena vault requires a cooldown period. Once a request to withdraw a specified
amount of USDe has been submitted, the alloted cooldown period must pass before the
withdraw USDe transaction can be submitted.

If an additional amount of USDe is requested to be withdrawn anytime before
withdrawing the originally requested amount, the cooldown period restarts.

Yield is not earned on USDe while in its cooldown period.

An allowance does not have to be set to initiate the cooldown period.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_ethena_request" method="post" path="/v1/ethena/request" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.ethena.ethena_request(amount=1.5, chain=models.EthenaRequestToWithdrawRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                           | Type                                                                                                                                                | Required                                                                                                                                            | Description                                                                                                                                         | Example                                                                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                                            | *Any*                                                                                                                                               | :heavy_check_mark:                                                                                                                                  | The amount of USDe to request to withdraw from Ethena's vault. If set to 'ALL', your total deposited USDe amount will be requested to be withdrawn. |                                                                                                                                                     |
| `chain`                                                                                                                                             | [models.EthenaRequestToWithdrawRequestChain](../../models/ethenarequesttowithdrawrequestchain.md)                                                   | :heavy_check_mark:                                                                                                                                  | N/A                                                                                                                                                 |                                                                                                                                                     |
| `sender`                                                                                                                                            | *str*                                                                                                                                               | :heavy_check_mark:                                                                                                                                  | The address of the transaction sender.                                                                                                              | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                          |
| `estimate_gas`                                                                                                                                      | *Optional[bool]*                                                                                                                                    | :heavy_minus_sign:                                                                                                                                  | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                        |                                                                                                                                                     |
| `retries`                                                                                                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                    | :heavy_minus_sign:                                                                                                                                  | Configuration to override the default retry behavior of the client.                                                                                 |                                                                                                                                                     |

### Response

**[models.EthenaRequestToWithdrawTransactionResponse](../../models/ethenarequesttowithdrawtransactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## ethena_unstake

Unstake deposited USDe from Ethena's vault.

Verify that the USDe being unstaked has completed its mandatory cooldown period
using the Ethena 'Get Vault & User Position' endpoint.

This is an all or nothing action. All of the USDe that has completed its cooldown
period must be withdrawn.

The passive yield earned on USDe deposits is represented by the increased value of
the shares received (sUSDe) upon depositing USDe. Trade in these shares in exchange
for the intial USDe deposited and any accrued yield since depositing.

An allowance does not have to be set to unstake USDe that has completed its cooldown
period.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_ethena_unstake" method="post" path="/v1/ethena/unstake" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.ethena.ethena_unstake(chain=models.EthenaUnstakeRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                      | [models.EthenaUnstakeRequestChain](../../models/ethenaunstakerequestchain.md)                                                | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `receiver`                                                                                                                   | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address which will receive the unstaked USDe. Defaults to the sender.                                                    |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |