# Universal
(*universal*)

## Overview

### Available Operations

* [generic_portfolio](#generic_portfolio) - List User Portfolio
* [generic_supported_chains](#generic_supported_chains) - List Supported Chains
* [generic_allowance](#generic_allowance) - Get Allowance
* [generic_ens](#generic_ens) - Resolve ENS
* [generic_wrap_eth](#generic_wrap_eth) - Wrap ETH
* [generic_unwrap_weth](#generic_unwrap_weth) - Unwrap WETH
* [generic_allowance_set](#generic_allowance_set) - Set Allowance

## generic_portfolio

Fetch the detailed portfolio of a specific wallet address on a given blockchain.

This includes the total value of the portfolio in USD and a breakdown of token
balances, including their respective values and quantities.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_generic_portfolio" method="get" path="/v1/generic/portfolio" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.universal.generic_portfolio(chain=models.V1GenericPortfolioChain.ARBITRUM, user="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                 | Type                                                                      | Required                                                                  | Description                                                               |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `chain`                                                                   | [models.V1GenericPortfolioChain](../../models/v1genericportfoliochain.md) | :heavy_check_mark:                                                        | N/A                                                                       |
| `user`                                                                    | *Optional[str]*                                                           | :heavy_minus_sign:                                                        | The user to get portfolio for.                                            |
| `retries`                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)          | :heavy_minus_sign:                                                        | Configuration to override the default retry behavior of the client.       |

### Response

**[models.Portfolio](../../models/portfolio.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## generic_supported_chains

Get the list of supported chains by the Compass API.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_generic_supported_chains" method="get" path="/v1/generic/supported_chains" -->
```python
from compass_api_sdk import CompassAPI


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.universal.generic_supported_chains()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `protocol`                                                          | [OptionalNullable[models.Protocol]](../../models/protocol.md)       | :heavy_minus_sign:                                                  | The protocol to get the supported chains for.                       |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.SupportedChainInfo](../../models/supportedchaininfo.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## generic_allowance

In decentralized finance (DeFi) protocols such as Uniswap or AAVE, users must set
a token allowance to authorize the protocol to spend a specified amount of their
tokens on their behalf.

This is a crucial step before engaging in any transactions or operations within
these protocols, ensuring that the protocol has the necessary permissions to manage
the user's tokens securely and efficiently.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_generic_allowance" method="get" path="/v1/generic/allowance" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.universal.generic_allowance(chain=models.V1GenericAllowanceChain.ARBITRUM, token="USDC", contract=models.V1GenericAllowanceContractEnum.SKY_USDS_VAULT, user="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                 | Type                                                                                      | Required                                                                                  | Description                                                                               | Example                                                                                   |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `chain`                                                                                   | [models.V1GenericAllowanceChain](../../models/v1genericallowancechain.md)                 | :heavy_check_mark:                                                                        | N/A                                                                                       |                                                                                           |
| `token`                                                                                   | *str*                                                                                     | :heavy_check_mark:                                                                        | The symbol or address of the token for which the allowance is checked.                    | USDC                                                                                      |
| `contract`                                                                                | [models.V1GenericAllowanceContractUnion](../../models/v1genericallowancecontractunion.md) | :heavy_check_mark:                                                                        | The name or address of the contract to check allowance for.                               |                                                                                           |
| `user`                                                                                    | *Optional[str]*                                                                           | :heavy_minus_sign:                                                                        | The user to get the ERC20 allowance of.                                                   |                                                                                           |
| `retries`                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                          | :heavy_minus_sign:                                                                        | Configuration to override the default retry behavior of the client.                       |                                                                                           |

### Response

**[models.AllowanceInfoResponse](../../models/allowanceinforesponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## generic_ens

An ENS name is a string ending in `.eth`.

E.g. `vitalik.eth`. This endpoint can be used to
query the actual ethereum wallet address behind the ENS name.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_generic_ens" method="get" path="/v1/generic/ens" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.universal.generic_ens(chain=models.V1GenericEnsChain.ETHEREUM, ens_name="vitalik.eth")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `chain`                                                             | [models.V1GenericEnsChain](../../models/v1genericenschain.md)       | :heavy_check_mark:                                                  | N/A                                                                 |
| `ens_name`                                                          | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | The ENS name to resolve.                                            |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.EnsNameInfoResponse](../../models/ensnameinforesponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## generic_wrap_eth

Wrapping ETH creates an ERC20 compliant form of ETH that is typically needed for
it to be traded on DeFi protocols.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_generic_wrap_eth" method="post" path="/v1/generic/wrap_eth" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.universal.generic_wrap_eth(amount=1.5, chain=models.WrapEthRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                     | [models.WrapEthRequestAmount](../../models/wrapethrequestamount.md)                                                          | :heavy_check_mark:                                                                                                           | The amount of ETH to wrap.                                                                                                   | 1.5                                                                                                                          |
| `chain`                                                                                                                      | [models.WrapEthRequestChain](../../models/wrapethrequestchain.md)                                                            | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
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

## generic_unwrap_weth

Unwrapping WETH converts the ERC-20 compliant form of ETH back to native ETH that
can be used for gas and other native purposes.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_generic_unwrap_weth" method="post" path="/v1/generic/unwrap_weth" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.universal.generic_unwrap_weth(amount=1.5, chain=models.UnwrapWethRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                     | [models.UnwrapWethRequestAmount](../../models/unwrapwethrequestamount.md)                                                    | :heavy_check_mark:                                                                                                           | The amount of WETH to unwrap.                                                                                                | 1.5                                                                                                                          |
| `chain`                                                                                                                      | [models.UnwrapWethRequestChain](../../models/unwrapwethrequestchain.md)                                                      | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
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

## generic_allowance_set

This endpoint allows users to modify the token allowance on any ERC-20 token for
a specific protocol.

In decentralized finance (DeFi), setting an allowance is a necessary step to
authorize a protocol to spend a specified amount of tokens on behalf of the user.
This operation is crucial for ensuring that the protocol can manage the user's
tokens securely and efficiently, enabling seamless transactions and operations
within the DeFi ecosystem.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_generic_allowance_set" method="post" path="/v1/generic/allowance/set" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.universal.generic_allowance_set(token="USDC", contract=models.SetAllowanceRequestContractEnum.AAVE_V3_POOL, amount=1.5, chain=models.SetAllowanceRequestChain.BASE, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token`                                                                                                                      | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The symbol or address of the token for which the allowance is set..                                                          | USDC                                                                                                                         |
| `contract`                                                                                                                   | [models.SetAllowanceRequestContractUnion](../../models/setallowancerequestcontractunion.md)                                  | :heavy_check_mark:                                                                                                           | The name or address of the contract to set spending allowance for.                                                           | AaveV3Pool                                                                                                                   |
| `amount`                                                                                                                     | [models.SetAllowanceRequestAmount](../../models/setallowancerequestamount.md)                                                | :heavy_check_mark:                                                                                                           | The amount to set the allowance to.                                                                                          | 1.5                                                                                                                          |
| `chain`                                                                                                                      | [models.SetAllowanceRequestChain](../../models/setallowancerequestchain.md)                                                  | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
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