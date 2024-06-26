# TimeSeriesInsights

> see https://aka.ms/autorest

This is the AutoRest configuration file for TimeSeriesInsights.

---

## Getting Started

To build the SDK for TimeSeriesInsights, simply [Install AutoRest](https://aka.ms/autorest/install) and in this folder, run:

> `autorest`

To see additional help and options, run:

> `autorest --help`

---

## Configuration

### Basic Information

These are the global settings for the TimeSeriesInsights API.

``` yaml
openapi-type: arm
tag: package-preview-2021-03
```


### Tag: package-preview-2021-03

These settings apply only when `--tag=package-preview-2021-03` is specified on the command line.

```yaml $(tag) == 'package-preview-2021-03'
input-file:
  - Microsoft.TimeSeriesInsights/preview/2021-03-31-preview/timeseriesinsights.json
```
### Tag: package-preview-2021-06

These settings apply only when `--tag=package-preview-2021-06` is specified on the command line.

``` yaml $(tag) == 'package-preview-2021-06'
input-file:
  - Microsoft.TimeSeriesInsights/preview/2021-06-30-preview/timeseriesinsights.json
```

### Tag: package-2020-05-15

These settings apply only when `--tag=package-2020-05-15` is specified on the command line.

``` yaml $(tag) == 'package-2020-05-15'
input-file:
- Microsoft.TimeSeriesInsights/stable/2020-05-15/timeseriesinsights.json
```

### Tag: package-2018-08-preview

These settings apply only when `--tag=package-2018-08-preview` is specified on the command line.

``` yaml $(tag) == 'package-2018-08-preview'
input-file:
- Microsoft.TimeSeriesInsights/preview/2018-08-15-preview/timeseriesinsights.json
```

### Tag: package-2017-11-15

These settings apply only when `--tag=package-2017-11-15` is specified on the command line.

``` yaml $(tag) == 'package-2017-11-15'
input-file:
- Microsoft.TimeSeriesInsights/stable/2017-11-15/timeseriesinsights.json
```

### Tag: package-2017-02-preview

These settings apply only when `--tag=package-2017-02-preview` is specified on the command line.

``` yaml $(tag) == 'package-2017-02-preview'
input-file:
- Microsoft.TimeSeriesInsights/preview/2017-02-28-preview/timeseriesinsights.json
```

## Suppression

``` yaml
directive:
  - suppress: READONLY_PROPERTY_NOT_ALLOWED_IN_REQUEST
    where: 
      - $.definitions.EnvironmentUpdateParameters.properties.kind
      - $.definitions.EventSourceUpdateParameters.properties.kind
    from: timeseriesinsights.json
    reason: This property is the discriminator for polymorph, but it can not be in request body.
  - suppress: OAV131 # DISCRIMINATOR_NOT_REQUIRED
    from: timeseriesinsights.json
    reason: kind is a non-settable property from the client in patch method.
  - suppress: R3025  # Tracked resource 'XXX' must have a get operation
    where:
      - $.definitions.StandardEnvironmentResource
      - $.definitions.LongTermEnvironmentResource
      - $.definitions.EventHubEventSourceResource
      - $.definitions.IoTHubEventSourceResource
      - $.definitions.Gen1EnvironmentResource
      - $.definitions.Gen2EnvironmentResource
    from: timeseriesinsights.json
    reason: These violations are false positives. The EventSources_Get operation returns an EventSourceResource, and both EventHubEventSourceResource and IoTHubEventSourceResource inherit from EventSourceResource. Similarly, the Environments_Get operation returns an EnvironmentResource, from which both StandardEnvironmentResource and LongTermEnvironmentResource inherit.

  - suppress: R3026  # Tracked resource 'XXX' must have patch operation that at least supports the update of tags. It's strongly recommended that the PATCH operation supports update of all mutable properties as well.
    where:
      - $.definitions.StandardEnvironmentResource
      - $.definitions.LongTermEnvironmentResource 
      - $.definitions.EventHubEventSourceResource
      - $.definitions.IoTHubEventSourceResource
      - $.definitions.Gen1EnvironmentResource
      - $.definitions.Gen2EnvironmentResource
    from: timeseriesinsights.json
    reason: These violations are false positives. The EventSources_Update operation takes an EventSourceUpdateParameters as the body, and EventHubEventSourceUpdateParameters and IoTHubEventSourceUpdateParameters both inherit from EventSourceUpdateParameters. Similarly, the Environments_Update operation takes an EnvironmentUpdateParameters as the body, and both StandardEnvironmentUpdateParameters and LongTermEnvironmentUpdateParameters inherit from EnvironmentUpdateParameters. These definitions can be used to update mutable properties of the event source, including the Tags collection.
  - suppress: R4009 # The response of operation:'PrivateEndpointConnections_CreateOrUpdate' is defined without 'systemData'. Consider adding the systemData to the response.
    from: timeseriesinsights.json
    reason: The systemData feature is not implemented in the Time Series Insights RP as of the publication of this api version.
```

---

# Code Generation

## Swagger to SDK

This section describes what SDK should be generated by the automatic system.
This is not used by Autorest itself.

``` yaml $(swagger-to-sdk)
swagger-to-sdk:
  - repo: azure-sdk-for-go
  - repo: azure-sdk-for-node
  - repo: azure-sdk-for-js
  - repo: azure-sdk-for-python-track2
  - repo: azure-resource-manager-schemas
  - repo: azure-powershell
```

## Go

See configuration in [readme.go.md](./readme.go.md)

## Java

These settings apply only when `--java` is specified on the command line.
Please also specify `--azure-libraries-for-java-folder=<path to the root directory of your azure-libraries-for-java clone>`.

``` yaml $(java)
azure-arm: true
fluent: true
namespace: com.microsoft.azure.management.timeseriesinsights
license-header: MICROSOFT_MIT_NO_CODEGEN
payload-flattening-threshold: 1
output-folder: $(azure-libraries-for-java-folder)/azure-mgmt-timeseriesinsights
```

## Python

See configuration in [readme.python.md](./readme.python.md)

### Java multi-api

``` yaml $(java) && $(multiapi)
batch:
  - tag: package-2017-11-15
  - tag: package-2017-02-preview
  - tag: package-2018-08-preview
  - tag: package-2020-05-15
```

### Tag: package-2017-11-15 and java

These settings apply only when `--tag=package-2017-11-15 --java` is specified on the command line.
Please also specify `--azure-libraries-for-java=<path to the root directory of your azure-sdk-for-java clone>`.

``` yaml $(tag) == 'package-2017-11-15' && $(java) && $(multiapi)
java:
  namespace: com.microsoft.azure.management.timeseriesinsights.v2017_11_15
  output-folder: $(azure-libraries-for-java-folder)/sdk/timeseriesinsights/mgmt-v2017_11_15
regenerate-manager: true
generate-interface: true
```

### Tag: package-2017-02-preview and java

These settings apply only when `--tag=package-2017-02-preview --java` is specified on the command line.
Please also specify `--azure-libraries-for-java=<path to the root directory of your azure-sdk-for-java clone>`.

``` yaml $(tag) == 'package-2017-02-preview' && $(java) && $(multiapi)
java:
  namespace: com.microsoft.azure.management.timeseriesinsights.v2017_02_28_preview
  output-folder: $(azure-libraries-for-java-folder)/sdk/timeseriesinsights/mgmt-v2017_02_28_preview
regenerate-manager: true
generate-interface: true
```

### Tag: package-2018-08-preview and java

These settings apply only when `--tag=package-2018-08-preview --java` is specified on the command line.
Please also specify `--azure-libraries-for-java=<path to the root directory of your azure-sdk-for-java clone>`.

``` yaml $(tag) == 'package-2018-08-preview' && $(java) && $(multiapi)
java:
  namespace: com.microsoft.azure.management.timeseriesinsights.v2018_08_15_preview
  output-folder: $(azure-libraries-for-java-folder)/sdk/timeseriesinsights/mgmt-v2018_08_15_preview
regenerate-manager: true
generate-interface: true
```

### Tag: package-2020-05-15 and java

These settings apply only when `--tag=package-2020-05-15 --java` is specified on the command line.
Please also specify `--azure-libraries-for-java=<path to the root directory of your azure-sdk-for-java clone>`.

``` yaml $(tag) == 'package-2020-05-15' && $(java) && $(multiapi)
java:
  namespace: com.microsoft.azure.management.timeseriesinsights.v2020_05_15
  output-folder: $(azure-libraries-for-java-folder)/sdk/timeseriesinsights/mgmt-v2020_05_15
regenerate-manager: true
generate-interface: true
```
