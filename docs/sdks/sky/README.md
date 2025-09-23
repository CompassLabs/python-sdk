# Sky
(*sky*)

## Overview

### Available Operations

* [sky_position](#sky_position) - Check USDS Position
* [sky_buy](#sky_buy) - Buy USDS
* [sky_sell](#sky_sell) - Sell USDS
* [sky_deposit](#sky_deposit) - Deposit USDS
* [sky_withdraw](#sky_withdraw) - Withdraw USDS

## sky_position

Check the USDS overall position.

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_sky_position" method="get" path="/v1/sky/position" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.sky.sky_position(chain=models.V1SkyPositionChain.ETHEREUM, user_address="0xacCEE9C7A5a759f814C7A770e2D8F78d662b1F60")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `chain`                                                             | [models.V1SkyPositionChain](../../models/v1skypositionchain.md)     | :heavy_check_mark:                                                  | N/A                                                                 |
| `user_address`                                                      | *str*                                                               | :heavy_check_mark:                                                  | The user-address of the desired position.                           |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.SkyCheckPositionResponse](../../models/skycheckpositionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## sky_buy

Buy USDS with DAI or USDC on a 1:1 basis. There are no fees.

If buying with DAI, user will need to set an allowance on the DAI contract for the
'SkyDaiUsdsConverter' contract beforehand.

If buying with USDC, user will need to set an allowance on the USDC contract for the
'SkyUsdcUsdsConverter' contract beforehand.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `SkyUsdcUsdsConverter`
 - `SkyDaiUsdsConverter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_sky_buy" method="post" path="/v1/sky/buy" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.sky.sky_buy(token_in=models.SkyBuyRequestTokenIn.USDC, amount=1.5, chain=models.SkyBuyRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token_in`                                                                                                                   | [models.SkyBuyRequestTokenIn](../../models/skybuyrequesttokenin.md)                                                          | :heavy_check_mark:                                                                                                           | The token you would like to swap 1:1 for USDS. Choose from DAI or USDC.                                                      |                                                                                                                              |
| `amount`                                                                                                                     | [models.SkyBuyRequestAmount](../../models/skybuyrequestamount.md)                                                            | :heavy_check_mark:                                                                                                           | The amount of USDS you would like to buy 1:1 with 'token_in'.                                                                | 1.5                                                                                                                          |
| `chain`                                                                                                                      | [models.SkyBuyRequestChain](../../models/skybuyrequestchain.md)                                                              | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
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

## sky_sell

Sell USDS for DAI or USDC on a 1:1 basis. There are no fees.

If swapping to DAI, user will need to set an allowance on the USDS contract for the
'SkyDaiUsdsConverter' contract beforehand.

If swapping to USDC, user will need to set an allowance on the USDS contract for the
'SkyUsdcUsdsConverter' contract beforehand.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `SkyUsdcUsdsConverter`
 - `SkyDaiUsdsConverter`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_sky_sell" method="post" path="/v1/sky/sell" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.sky.sky_sell(token_out=models.SkySellRequestTokenOut.DAI, amount=1.5, chain=models.SkySellRequestChain.ETHEREUM, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `token_out`                                                                                                                  | [models.SkySellRequestTokenOut](../../models/skysellrequesttokenout.md)                                                      | :heavy_check_mark:                                                                                                           | The token you would like to swap 1:1 with USDS. Choose from DAI or USDC.                                                     |                                                                                                                              |
| `amount`                                                                                                                     | [models.SkySellRequestAmount](../../models/skysellrequestamount.md)                                                          | :heavy_check_mark:                                                                                                           | The amount of USDS you would like to sell 1:1 for 'token_out'.                                                               | 1.5                                                                                                                          |
| `chain`                                                                                                                      | [models.SkySellRequestChain](../../models/skysellrequestchain.md)                                                            | :heavy_check_mark:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
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

## sky_deposit

Deposit USDS to earn yield. Deposited USDS is represented as sUSDS.

Allowance must be set on USDS contract for UsdsVault.

There are no fees.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `SkyUsdsVault`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_sky_deposit" method="post" path="/v1/sky/deposit" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.sky.sky_deposit(amount=1.5, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", chain=models.SkyDepositRequestChain.ETHEREUM, estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                     | [models.SkyDepositRequestAmount](../../models/skydepositrequestamount.md)                                                    | :heavy_check_mark:                                                                                                           | The amount of USDS you would like to deposit for sUSDS to earn yield.                                                        | 1.5                                                                                                                          |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `receiver`                                                                                                                   | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address which will receive the sUSDS. Defaults to the sender.                                                            |                                                                                                                              |
| `chain`                                                                                                                      | [Optional[models.SkyDepositRequestChain]](../../models/skydepositrequestchain.md)                                            | :heavy_minus_sign:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |

## sky_withdraw

Withdraw USDS. Exchange yield-bearing sUSDS for USDS.

Allowance must be set on USDS contract for UsdsVault.

There are no fees.
                    <Info>
                    **Required Allowances**

                        In order to make this transaction, token allowances need to be set for the following contracts.

                     - `SkyUsdsVault`
                    </Info>
                

### Example Usage

<!-- UsageSnippet language="python" operationID="v1_sky_withdraw" method="post" path="/v1/sky/withdraw" -->
```python
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.sky.sky_withdraw(amount=4514.13, sender="0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B", chain=models.SkyWithdrawRequestChain.ETHEREUM, estimate_gas=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                    | Type                                                                                                                         | Required                                                                                                                     | Description                                                                                                                  | Example                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                     | *Any*                                                                                                                        | :heavy_check_mark:                                                                                                           | The amount of USDS you would like to withdraw. If set to 'ALL', your total deposited USDS amount will be withdrawn.          |                                                                                                                              |
| `sender`                                                                                                                     | *str*                                                                                                                        | :heavy_check_mark:                                                                                                           | The address of the transaction sender.                                                                                       | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                                                   |
| `receiver`                                                                                                                   | *OptionalNullable[str]*                                                                                                      | :heavy_minus_sign:                                                                                                           | The address which will receive the withdrawn USDS. Defaults to the sender.                                                   |                                                                                                                              |
| `chain`                                                                                                                      | [Optional[models.SkyWithdrawRequestChain]](../../models/skywithdrawrequestchain.md)                                          | :heavy_minus_sign:                                                                                                           | N/A                                                                                                                          |                                                                                                                              |
| `estimate_gas`                                                                                                               | *Optional[bool]*                                                                                                             | :heavy_minus_sign:                                                                                                           | Determines whether to estimate gas costs for transactions, also verifying that the transaction can be successfully executed. |                                                                                                                              |
| `retries`                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                             | :heavy_minus_sign:                                                                                                           | Configuration to override the default retry behavior of the client.                                                          |                                                                                                                              |

### Response

**[models.TransactionResponse](../../models/transactionresponse.md)**

### Errors

| Error Type                 | Status Code                | Content Type               |
| -------------------------- | -------------------------- | -------------------------- |
| errors.HTTPValidationError | 422                        | application/json           |
| errors.APIError            | 4XX, 5XX                   | \*/\*                      |