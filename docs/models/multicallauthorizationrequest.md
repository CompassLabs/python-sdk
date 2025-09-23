# MulticallAuthorizationRequest

Request model for getting a multicall authorization.

This model is used to authorize a sender address to perform multicall operations,
allowing it to call multiple functions on multiple contracts in a single
transaction.


## Fields

| Field                                                                                        | Type                                                                                         | Required                                                                                     | Description                                                                                  | Example                                                                                      |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `chain`                                                                                      | [models.MulticallAuthorizationRequestChain](../models/multicallauthorizationrequestchain.md) | :heavy_check_mark:                                                                           | N/A                                                                                          |                                                                                              |
| `sender`                                                                                     | *str*                                                                                        | :heavy_check_mark:                                                                           | The Ethereum address to use for authorization                                                | 0x29F20a192328eF1aD35e1564aBFf4Be9C5ce5f7B                                                   |