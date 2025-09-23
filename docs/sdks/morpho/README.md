# Morpho
(*morpho*)

## Overview

### Available Operations

* [morpho_vaults](#morpho_vaults) - Get Vaults
* [morpho_vault](#morpho_vault) - Get Vault & User Position
* [morpho_markets](#morpho_markets) - Get Markets
* [morpho_market](#morpho_market) - Get Market
* [morpho_market_position](#morpho_market_position) - Check Market Position
* [morpho_user_position](#morpho_user_position) - Check User Position
* [morpho_deposit](#morpho_deposit) - Deposit to Vault
* [morpho_withdraw](#morpho_withdraw) - Withdraw from Vault
* [morpho_supply_collateral](#morpho_supply_collateral) - Supply Collateral to Market
* [morpho_withdraw_collateral](#morpho_withdraw_collateral) - Withdraw Collateral from Market
* [morpho_borrow](#morpho_borrow) - Borrow from Market
* [morpho_repay](#morpho_repay) - Repay to Market

## morpho_vaults

Query a list of vaults you can deposit into.

Each vault has one unique token that can be deposited. In exchange for depositing
tokens into a vault you receive shares. You earn yield on these shares by their
exchange value increasing over time.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_vaults" method="get" path="/v1/morpho/vaults" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_vaults(chain=models.V1MorphoVaultsChain.BASE, deposit_token="USDC")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                       | Type                                                                            | Required                                                                        | Description                                                                     | Example                                                                         |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `chain`                                                                         | [models.V1MorphoVaultsChain](../../models/v1morphovaultschain.md)               | :heavy_check_mark:                                                              | N/A                                                                             |                                                                                 |
| `deposit_token`                                                                 | *OptionalNullable[str]*                                                         | :heavy_minus_sign:                                                              | Symbol or address of the deposit token to filter vaults by. Optional parameter. | USDC                                                                            |
| `retries`                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                | :heavy_minus_sign:                                                              | Configuration to override the default retry behavior of the client.             |                                                                                 |

### Response

**[models.MorphoGetVaultsResponse](../../models/morphogetvaultsresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## morpho_vault

Get Vault data & User Position.

The user position is only included if 'user_address' parameter is included.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_vault" method="get" path="/v1/morpho/vault" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_vault(chain=models.V1MorphoVaultChain.ETHEREUM, vault_address="0x182863131F9a4630fF9E27830d945B1413e347E8")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                      | Type                                                                                                                                           | Required                                                                                                                                       | Description                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `chain`                                                                                                                                        | [models.V1MorphoVaultChain](../../models/v1morphovaultchain.md)                                                                                | :heavy_check_mark:                                                                                                                             | N/A                                                                                                                                            |
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

## morpho_markets

Query a list of markets you can borrow from.

Each market has one unique token that can be borrowed against one unique token that
can be used as collateral.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_markets" method="get" path="/v1/morpho/markets" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_markets(chain=models.V1MorphoMarketsChain.BASE, collateral_token="USDC", loan_token="USDC")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                           | Type                                                                                | Required                                                                            | Description                                                                         | Example                                                                             |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `chain`                                                                             | [models.V1MorphoMarketsChain](../../models/v1morphomarketschain.md)                 | :heavy_check_mark:                                                                  | N/A                                                                                 |                                                                                     |
| `collateral_token`                                                                  | *OptionalNullable[str]*                                                             | :heavy_minus_sign:                                                                  | Symbol or address of the collateral token to filter markets by. Optional parameter. | USDC                                                                                |
| `loan_token`                                                                        | *OptionalNullable[str]*                                                             | :heavy_minus_sign:                                                                  | Symbol or address of the loan token to filter markets by. Optional parameter.       | USDC                                                                                |
| `retries`                                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                    | :heavy_minus_sign:                                                                  | Configuration to override the default retry behavior of the client.                 |                                                                                     |

### Response

**[models.MorphoGetMarketsResponse](../../models/morphogetmarketsresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## morpho_market

Get data & metrics for a specific Morpho market.

Including:
- Current, daily, weekly, monthly, yearly APY
- Collateral & loan asset data
- Liquidation loan-to-value ratio
- Collateral, borrow & liquidity value
- Utilization ratio
- Pertinent metadata
- Whitelist status

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_market" method="get" path="/v1/morpho/market" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_market(chain=models.V1MorphoMarketChain.BASE, unique_market_key="0x3b3769cfca57be2eaed03fcc5299c25691b77781a1e124e7a8d520eb9a7eabb5")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                        | Type                                                                                             | Required                                                                                         | Description                                                                                      |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `chain`                                                                                          | [models.V1MorphoMarketChain](../../models/v1morphomarketchain.md)                                | :heavy_check_mark:                                                                               | N/A                                                                                              |
| `unique_market_key`                                                                              | *str*                                                                                            | :heavy_check_mark:                                                                               | The key that uniquely identifies the market. This can be found using the 'Get Markets' endpoint. |
| `retries`                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                 | :heavy_minus_sign:                                                                               | Configuration to override the default retry behavior of the client.                              |

### Response

**[models.MorphoGetMarketResponse](../../models/morphogetmarketresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## morpho_market_position

Check how many shares you've borrowed and the equivalent token amount of a given
market.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_market_position" method="get" path="/v1/morpho/market_position" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_market_position(chain=models.V1MorphoMarketPositionChain.BASE, user_address="0x81d310Eb515E05EB26322e2DeDE9e75b754885A4", unique_market_key="0x3b3769cfca57be2eaed03fcc5299c25691b77781a1e124e7a8d520eb9a7eabb5")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                        | Type                                                                                             | Required                                                                                         | Description                                                                                      |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| `chain`                                                                                          | [models.V1MorphoMarketPositionChain](../../models/v1morphomarketpositionchain.md)                | :heavy_check_mark:                                                                               | N/A                                                                                              |
| `user_address`                                                                                   | *str*                                                                                            | :heavy_check_mark:                                                                               | The user address of the desired market position.                                                 |
| `unique_market_key`                                                                              | *str*                                                                                            | :heavy_check_mark:                                                                               | The key that uniquely identifies the market. This can be found using the 'Get Markets' endpoint. |
| `retries`                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                 | :heavy_minus_sign:                                                                               | Configuration to override the default retry behavior of the client.                              |

### Response

**[models.MorphoCheckMarketPositionResponse](../../models/morphocheckmarketpositionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## morpho_user_position

Check user's overall position across the entire Morpho ecosystem.

Inlcuding all vault and market position metrics and relavant metadata of said vaults
and markets.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_user_position" method="get" path="/v1/morpho/user_position" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_user_position(chain=models.V1MorphoUserPositionChain.BASE, user_address="0x81d310Eb515E05EB26322e2DeDE9e75b754885A4")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                     | Type                                                                          | Required                                                                      | Description                                                                   |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `chain`                                                                       | [models.V1MorphoUserPositionChain](../../models/v1morphouserpositionchain.md) | :heavy_check_mark:                                                            | N/A                                                                           |
| `user_address`                                                                | *str*                                                                         | :heavy_check_mark:                                                            | The user wallet address of the desired user position.                         |
| `retries`                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)              | :heavy_minus_sign:                                                            | Configuration to override the default retry behavior of the client.           |

### Response

**[models.MorphoCheckUserPositionResponse](../../models/morphocheckuserpositionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## morpho_deposit

Deposit tokens into a Morpho Vault to earn passive yield from interest paid by
borrowers.

Each vault accepts one unique token that can be deposited.

A Morpho Vault has one loan asset and can allocate deposits to multiple Morpho
markets. Users can deposit into a vault to start earning passive yield from interest
paid by borrowers. Vaults feature automated risk management, actively curating risk
exposure for all deposited assets so users don't need to make these decisions
themselves. Users maintain full control over their assets, can monitor the vault's
state at any time, and withdraw their liquidity at their discretion.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `<vault-contract-address>`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_deposit" method="post" path="/v1/morpho/deposit" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_deposit(vault_address="0xbEef047a543E45807105E51A8BBEFCc5950fcfBa", amount=1.5, chain=models.MorphoDepositRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vault_address`                                                                                                                                   | *str*                                                                                                                                             | :heavy_check_mark:                                                                                                                                | The vault address you are depositing to.                                                                                                          | 0xbEef047a543E45807105E51A8BBEFCc5950fcfBa                                                                                                        |
| `amount`                                                                                                                                          | [models.MorphoDepositRequestAmount](../../models/morphodepositrequestamount.md)                                                                   | :heavy_check_mark:                                                                                                                                | The amount of tokens to deposit into the vault.                                                                                                   | 1.5                                                                                                                                               |
| `chain`                                                                                                                                           | [models.MorphoDepositRequestChain](../../models/morphodepositrequestchain.md)                                                                     | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               |                                                                                                                                                   |
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

## morpho_withdraw

Withdraw deposited tokens from a Morpho Vault.

The passive yield earned on token deposits is represented by the increased value of
the shares received upon depositing tokens.

A Morpho Vault has one loan asset and can allocate deposits to multiple Morpho
markets. Users can deposit into a vault to start earning passive yield from interest
paid by borrowers. Vaults feature automated risk management, actively curating risk
exposure for all deposited assets so users don't need to make these decisions
themselves. Users maintain full control over their assets, can monitor the vault's
state at any time, and withdraw their liquidity at their discretion.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_withdraw" method="post" path="/v1/morpho/withdraw" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_withdraw(vault_address="0xbEef047a543E45807105E51A8BBEFCc5950fcfBa", amount="1.5", chain=models.MorphoWithdrawRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `vault_address`                                                                                                              | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The vault address you are withdrawing from.                                                                                  | 0xbEef047a543E45807105E51A8BBEFCc5950fcfBa                                                                                   |
| `amount`                                                                                                                     | *Any*                                                                                                                        | :heavy_check_mark:                                                                                                           | The amount of tokens to withdraw from the vault. If set to 'ALL', your total deposited token amount will be withdrawn.       |                                                                                                                              |
| `chain`                                                                                                                      | [models.MorphoWithdrawRequestChain](../../models/morphowithdrawrequestchain.md)                                              | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
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

## morpho_supply_collateral

Supply collateral to a Morpho Market in order to borrow against it.

A Morpho Market is a primitive lending pool that pairs one collateral asset with one
loan asset. Each market is isolated (meaning risks are contained within each
individual market), immutable (cannot be changed after deployment), and will persist
as long as the blockchain it is deployed on is live.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `Morpho`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_supply_collateral" method="post" path="/v1/morpho/supply_collateral" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_supply_collateral(amount=1.5, unique_market_key="0xe7399fdebc318d76dfec7356caafcf8cd4b91287e139a3ec423f09aeeb656fc4", chain=models.MorphoSupplyCollateralRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                     | [models.MorphoSupplyCollateralRequestAmount](../../models/morphosupplycollateralrequestamount.md)                            | :heavy_check_mark:                                                                                                           | Amount of the token to supply to the market as collateral.                                                                   | 1.5                                                                                                                          |
| `unique_market_key`                                                                                                          | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The key that uniquely identifies the market. This can be found using the 'Get Markets' endpoint.                             | 0xe7399fdebc318d76dfec7356caafcf8cd4b91287e139a3ec423f09aeeb656fc4                                                           |
| `chain`                                                                                                                      | [models.MorphoSupplyCollateralRequestChain](../../models/morphosupplycollateralrequestchain.md)                              | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `on_behalf_of`                                                                                                               | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address on behalf of whom the supplied collateral is made. Defaults to sender.                                           |                                                                                                                              |
| `callback_data`                                                                                                              | *OptionalNullable[bytes]*                                                                                                    | :heavy_minus_sign:                                                                                                           | An optional field for callback byte data that will be triggered upon successful supplying of collateral.                     |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## morpho_withdraw_collateral

Withdraw collateral that has been supplied to a Morpho Market.

A Morpho Market is a primitive lending pool that pairs one collateral asset with one
loan asset. Each market is isolated (meaning risks are contained within each
individual market), immutable (cannot be changed after deployment), and will persist
as long as the blockchain it is deployed on is live.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `Morpho`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_withdraw_collateral" method="post" path="/v1/morpho/withdraw_collateral" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_withdraw_collateral(amount=1.5, unique_market_key="0xe7399fdebc318d76dfec7356caafcf8cd4b91287e139a3ec423f09aeeb656fc4", chain=models.MorphoWithdrawCollateralRequestChain.ARBITRUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                     | [models.MorphoWithdrawCollateralRequestAmount](../../models/morphowithdrawcollateralrequestamount.md)                        | :heavy_check_mark:                                                                                                           | Amount of the token to supply to the market as collateral.                                                                   | 1.5                                                                                                                          |
| `unique_market_key`                                                                                                          | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The key that uniquely identifies the market. This can be found using the 'Get Markets' endpoint.                             | 0xe7399fdebc318d76dfec7356caafcf8cd4b91287e139a3ec423f09aeeb656fc4                                                           |
| `chain`                                                                                                                      | [models.MorphoWithdrawCollateralRequestChain](../../models/morphowithdrawcollateralrequestchain.md)                          | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `on_behalf_of`                                                                                                               | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address on behalf of whom the withdraw is made. Defaults to sender.                                                      |                                                                                                                              |
| `receiver`                                                                                                                   | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address where the withdrawn collateral will be received. Defaults to sender.                                             |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## morpho_borrow

Borrow tokens from a Morpho Market against supplied collateral.

The position could be liquidated when a borrower's Loan-To-Value (LTV) exceeds the
Liquidation Loan-To-Value (LLTV) threshold of the market.

A Morpho Market is a primitive lending pool that pairs one collateral asset with one
loan asset. Each market is isolated (meaning risks are contained within each
individual market), immutable (cannot be changed after deployment), and will persist
as long as the blockchain it is deployed on is live.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `Morpho`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_borrow" method="post" path="/v1/morpho/borrow" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_borrow(amount=1.5, unique_market_key="0xe7399fdebc318d76dfec7356caafcf8cd4b91287e139a3ec423f09aeeb656fc4", chain=models.MorphoBorrowRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                     | [models.MorphoBorrowRequestAmount](../../models/morphoborrowrequestamount.md)                                                | :heavy_check_mark:                                                                                                           | Amount of the token to borrow from the market.                                                                               | 1.5                                                                                                                          |
| `unique_market_key`                                                                                                          | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The key that uniquely identifies the market. This can be found using the 'Get Markets' endpoint.                             | 0xe7399fdebc318d76dfec7356caafcf8cd4b91287e139a3ec423f09aeeb656fc4                                                           |
| `chain`                                                                                                                      | [models.MorphoBorrowRequestChain](../../models/morphoborrowrequestchain.md)                                                  | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `on_behalf_of`                                                                                                               | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address where the collateral is borrowed against. Defaults to sender.                                                    |                                                                                                                              |
| `receiver`                                                                                                                   | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address of the receiver of the tokens borrowed. Defaults to the transaction sender.                                      |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## morpho_repay

Repay borrowed tokens to a market in order to reduce or eliminate debt.

A Morpho Market is a primitive lending pool that pairs one collateral asset with one
loan asset. Each market is isolated (meaning risks are contained within each
individual market), immutable (cannot be changed after deployment), and will persist
as long as the blockchain it is deployed on is live.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `Morpho`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_morpho_repay" method="post" path="/v1/morpho/repay" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.morpho.morpho_repay(amount=1.5, unique_market_key="0xe7399fdebc318d76dfec7356caafcf8cd4b91287e139a3ec423f09aeeb656fc4", chain=models.MorphoRepayRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                         | Type                                                                                                                                                              | Required                                                                                                                                                          | Description                                                                                                                                                       | Example                                                                                                                                                           |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                                                          | *Any*                                                                                                                                                             | :heavy_check_mark:                                                                                                                                                | Amount of the token to repay to the market. If set to 'ALL', all debt plus interest will be paid back if the user has a sufficient token balance in their wallet. |                                                                                                                                                                   |
| `unique_market_key`                                                                                                                                               | *str*                                                                                                                                                             | :heavy_check_mark:                                                                                                                                                | The key that uniquely identifies the market. This can be found using the 'Get Markets' endpoint.                                                                  | 0xe7399fdebc318d76dfec7356caafcf8cd4b91287e139a3ec423f09aeeb656fc4                                                                                                |
| `chain`                                                                                                                                                           | [models.MorphoRepayRequestChain](../../models/morphorepayrequestchain.md)                                                                                         | :heavy_check_mark:                                                                                                                                                | N/A                                                                                                                                                               |                                                                                                                                                                   |
| `sender`                                                                                                                                                          | *str*                                                                                                                                                             | :heavy_check_mark:                                                                                                                                                | The address of the transaction sender.                                                                                                                            | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                                                        |
| `on_behalf_of`                                                                                                                                                    | *OptionalNullable[str]*                                                                                                                                           | :heavy_minus_sign:                                                                                                                                                | The address on behalf of whom the repayment is made. Defaults to sender.                                                                                          |                                                                                                                                                                   |
| `callback_data`                                                                                                                                                   | *OptionalNullable[bytes]*                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                | An optional field for callback byte data that will be triggered upon successful repaying of debt.                                                                 |                                                                                                                                                                   |
| `estimate_gas`                                                                                                                                                    | *Optional[bool]*                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed.                                      |                                                                                                                                                                   |
| `retries`                                                                                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                  | :heavy_minus_sign:                                                                                                                                                | Configuration to override the default retry behavior of the client.                                                                                               |                                                                                                                                                                   |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |