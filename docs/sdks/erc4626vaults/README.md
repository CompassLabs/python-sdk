# ERC4626Vaults
(*erc_4626_vaults*)

## Overview

### Available Operations

* [vaults_vault](#vaults_vault) - Get Vault & User Position
* [vaults_deposit](#vaults_deposit) - Deposit to Vault
* [vaults_withdraw](#vaults_withdraw) - Withdraw from Vault

## vaults_vault

Get Vault data & User Position.

The user position is only included if 'user_address' parameter is included.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_vaults_vault" method="get" path="/v1/vaults/vault" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.erc_4626_vaults.vaults_vault(chain=models.V1VaultsVaultChain.ETHEREUM, vault_address="0x182863131F9a4630fF9E27830d945B1413e347E8")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                      | Type                                                                                                                                           | Required                                                                                                                                       | Description                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                                        | [models.V1VaultsVaultChain](../../models/v1vaultsvaultchain.md)                                                                                | :heavy_check_mark:                                                                                                                             | N/A                                                                                                                                            |
| `vault_address`                                                                                                                                | *str*                                                                                                                                          | :heavy_check_mark:                                                                                                                             | The vault address of the desired vault position.                                                                                               |
| `block`                                                                                                                                        | *OptionalNullable[int]*                                                                                                                        | :heavy_minus_sign:                                                                                                                             | Optional block number (defaults to latest).                                                                                                    |
| `user_address`                                                                                                                                 | *OptionalNullable[str]*                                                                                                                        | :heavy_minus_sign:                                                                                                                             | The user address of the desired vault position. Only include if you would like the user position included in the response. Defaults to `None`. |
| `retries`                                                                                                                                      | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                               | :heavy_minus_sign:                                                                                                                             | Configuration to override the default retry behavior of the client.                                                                            |

### Response

**[models.VaultGetVaultResponse](../../models/vaultgetvaultresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## vaults_deposit

Deposit tokens into a Vault (ERC-4626 Standard) to earn passive yield.

Each vault accepts one unique token that can be deposited.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `<vault_address>`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_vaults_deposit" method="post" path="/v1/vaults/deposit" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.erc_4626_vaults.vaults_deposit(vault_address="0xbEef047a543E45807105E51A8BBEFCc5950fcfBa", amount=1.5, chain=models.VaultDepositRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vault_address`                                                                                                                                   | *str*                                                                                                                                             | :heavy_check_mark:                                                                                                                                | The vault address you are depositing to.                                                                                                          | 0xbEef047a543E45807105E51A8BBEFCc5950fcfBa                                                                                                        |
| `amount`                                                                                                                                          | [models.VaultDepositRequestAmount](../../models/vaultdepositrequestamount.md)                                                                     | :heavy_check_mark:                                                                                                                                | The amount of tokens to deposit into the vault.                                                                                                   | 1.5                                                                                                                                               |
| `chain`                                                                                                                                           | [models.VaultDepositRequestChain](../../models/vaultdepositrequestchain.md)                                                                       | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               |                                                                                                                                                   |
| `sender`                                                                                                                                          | *str*                                                                                                                                             | :heavy_check_mark:                                                                                                                                | The address of the transaction sender.                                                                                                            | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                        |
| `receiver`                                                                                                                                        | *OptionalNullable[str]*                                                                                                                           | :heavy_minus_sign:                                                                                                                                | The address which will receive the shares from the vault representing their proportional ownership of the vault's assets. Defaults to the sender. |                                                                                                                                                   |
| `estimate_gas`                                                                                                                                    | *Optional[bool]*                                                                                                                                  | :heavy_minus_sign:                                                                                                                                | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                      |                                                                                                                                                   |
| `retries`                                                                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                  | :heavy_minus_sign:                                                                                                                                | Configuration to override the default retry behavior of the client.                                                                               |                                                                                                                                                   |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## vaults_withdraw

Withdraw deposited tokens from a Vault (ERC-4626 Standard).

The passive yield earned on token deposits is represented by the increased value of
the shares received upon depositing tokens. Trade in these shares for the tokens you
deposited plus any accrued yield.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_vaults_withdraw" method="post" path="/v1/vaults/withdraw" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.erc_4626_vaults.vaults_withdraw(vault_address="0xbEef047a543E45807105E51A8BBEFCc5950fcfBa", amount=1.5, chain=models.VaultWithdrawRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `vault_address`                                                                                                              | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The vault address you are withdrawing from.                                                                                  | 0xbEef047a543E45807105E51A8BBEFCc5950fcfBa                                                                                   |
| `amount`                                                                                                                     | *Any*                                                                                                                        | :heavy_check_mark:                                                                                                           | The amount of tokens to withdraw from the vault. If set to 'ALL', your total deposited token amount will be withdrawn.       |                                                                                                                              |
| `chain`                                                                                                                      | [models.VaultWithdrawRequestChain](../../models/vaultwithdrawrequestchain.md)                                                | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `receiver`                                                                                                                   | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address which will receive the tokens withdrawn. Defaults to the sender.                                                 |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |