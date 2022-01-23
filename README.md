# AzGather - Gather Azure environment info

[![Action-Test](https://github.com/AzActions/AzGather/actions/workflows/Action-Test.yml/badge.svg)](https://github.com/AzActions/AzGather/actions/workflows/Action-Test.yml)

[![Linter](https://github.com/AzActions/AzGather/workflows/Linter/badge.svg)](https://github.com/AzActions/AzGather/actions/workflows/Linter.yml)

[![GitHub](https://img.shields.io/github/license/AzActions/AzGather)](LICENSE)

This action gathers environment info from Azure and stores it as systems environment variables in runner.

## Why use this module?

For environments which have resources in place which other deployments connect to or relies on, the AzGather task will get a predefined set of variables for use in later deployments.
This allows for a dynamic deployment and is created to simplify onboarding to solutions created and shared by a central team in a known environment.

## Inputs

N/A

## Outputs

N/A

## Environment variables

This action creates the following environment variables on the runner.

| Variable name        | Description                                                                            |
| :------------------- | :------------------------------------------------------------------------------------- |
| `EnvironmentID`      | The Azure subscription name prefix in the current context.                             |
| `Monitoring_RGName`  | The name of the resource group used for monitoring and IaaS management.                |
| `Monitoring_RGID`    | The resourceID of the resource group used for monitoring and IaaS management.          |
| `Monitoring_LAWName` | The name of the Log Analytics workspace used for monitoring and IaaS management.       |
| `Monitoring_LAWID`   | The resourceID of the Log Analytics workspace used for monitoring and IaaS management. |
| `Monitoring_AAName`  | The name of the Automation Account used for monitoring and IaaS management.            |
| `Monitoring_AAID`    | The resourceID of the Automation Account used for monitoring and IaaS management.      |

## Usage

```yaml
name: Test-Workflow

on: [push]

env:
  TenantID: ${{ secrets.TENANT_ID }}
  AppID: ${{ secrets.APP_ID }}
  Subscription: ${{ secrets.AUBSCRIPTION_ID }}
  AppSecret: ${{ secrets.APP_SECRET }}

jobs:
  DefaultTest:
    runs-on: ubuntu-latest
    steps:

      - name: Connect to Azure
        uses: AzActions/AzConnect@v1

      - name: Gather environment information
        uses: AzActions/AzGather@v1
```

## Dependencies

- [AzActions/AzUtilities](https://www.github.com/AzActions/AzUtilities)
- Depends access to an Azure Environment through the [AzActions/AzConnect](https://github.com/AzActions/AzConnect) action using Azure CLI, which is the default behaviour.

## Contributing

This project welcomes contributions and suggestions. Please review [How to contribute](https://github.com/AzActions/AzActions#how-to-contibute) on our [AzActions](https://github.com/AzActions/AzActions) page.
