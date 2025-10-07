<!-- Start SDK Example Usage [usage] -->
```python
# Synchronous Example
from compass_api_sdk import CompassAPI, models


with CompassAPI(
    api_key_auth="<YOUR_API_KEY_HERE>",
) as compass_api:

    res = compass_api.aave_v3.aave_aave_supported_tokens(chain=models.V1AaveAaveSupportedTokensChain.ARBITRUM)

    # Handle response
    print(res)
```

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.

```python
# Asynchronous Example
import asyncio
from compass_api_sdk import CompassAPI, models

async def main():

    async with CompassAPI(
        api_key_auth="<YOUR_API_KEY_HERE>",
    ) as compass_api:

        res = await compass_api.aave_v3.aave_aave_supported_tokens_async(chain=models.V1AaveAaveSupportedTokensChain.ARBITRUM)

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->