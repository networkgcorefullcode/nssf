<!--
SPDX-FileCopyrightText: 2021 Open Networking Foundation <info@opennetworking.org>
Copyright 2019 free5GC.org

SPDX-License-Identifier: Apache-2.0
-->
[![Go Report Card](https://goreportcard.com/badge/github.com/omec-project/nssf)](https://goreportcard.com/report/github.com/omec-project/nssf)

# NSSF

Compliance of the 5G Network functions can be found at [5G Compliance](https://docs.sd-core.opennetworking.org/main/overview/3gpp-compliance-5g.html)

## Repository Structure

Below is a high-level view of the repository and its main components:
```
.
├── consumer                    # Implements NSSF’s communication with other Network Functions (NFs), mainly for NF management and registration through the NRF.
│   ├── nf_management.go
│   └── nf_management_test.go
├── context                     # Manages internal NSSF runtime data, including context structures for slice selection and NF registration.
│   └── context.go
├── dev-container.ps1
├── dev-container.sh
├── DEV_README.md
├── Dockerfile
├── Dockerfile_dev
├── Dockerfile.fast
├── factory                     # Handles configuration initialization, file loading, and default parameter setup for the NSSF service. Includes test files for configuration validation.
│   ├── config.go
│   ├── factory.go
│   ├── manual_config.go
│   └── nssf_config_test.go
├── go.mod
├── go.mod.license
├── go.sum
├── go.sum.license
├── LICENSES
│   └── Apache-2.0.txt
├── logger                      # Provides a unified logging interface used across the NSSF for debugging and operational tracing.
│   └── logger.go
├── Makefile
├── metrics                     # Collects and exposes telemetry and monitoring data to external observability systems.
│   └── telemetry.go
├── nfregistration              # Contains logic for NSSF registration, discovery, and lifecycle management within the NRF.
│   ├── nf_registration.go
│   └── nf_registration_test.go
├── NOTICE.txt
├── nssaiavailability           # Implements APIs and logic to manage NSSAI (Network Slice Selection Assistance Information) availability and subscription handling for network slices.
│   ├── api_nf_instance_id_document.go
│   ├── api_subscription_id_document.go
│   ├── api_subscriptions_collection.go
│   └── routers.go
├── nsselection                 # Provides APIs for network slice selection operations — determining the appropriate slice for UE registration or PDU session requests.
│   ├── api_network_slice_information_document.go
│   └── routers.go
├── nssf.go
├── plugin                      # Contains helper modules that extend NSSF functionality, such as parameter patching and NS selection query parsing.
│   ├── nsselection_query_parameter.go
│   └── patch_document.go
├── polling                     # Periodically polls configuration data and monitors changes in NF registration or operational state.
│   ├── nf_configuration.go
│   └── nf_configuration_test.go
├── producer                    # Implements the core NSSF logic for producing responses to slice selection and availability queries from consumers (e.g., AMF).
│   ├── network_slice_information_document.go
│   ├── nf_instance_id_document.go
│   ├── nssaiavailability_store.go
│   ├── nssaiavailability_subscription.go
│   ├── nsselection_for_pdu_session.go
│   ├── nsselection_for_registration.go
│   ├── subscription_id_document.go
│   └── subscriptions_collection.go
├── README.md
├── service                     # Initializes and starts the NSSF service; contains entry points for server setup and API registration.
│   └── init.go
├── Taskfile.yml
├── test                        # Holds unit tests and configuration examples to validate NSSF behavior, including sample YAML configurations for testing.
│   ├── conf
│   │   ├── test_nssf_config_with_custom_webui_url.yaml
│   │   └── test_nssf_config.yaml
│   ├── param.go
│   └── util.go
├── test-mirror.txt
├── util                        # General-purpose utility functions used across the repository (e.g., for data conversion, helper methods, and testing utilities).
│   ├── util_func.go
│   ├── util.go
│   └── util_test.go
├── VERSION
└── VERSION.license

17 directories, 56 files
```

## Configuration and Deployment

**Docker**

To build the container image:
```
task mod-start
task build
task docker-build-fast
```

**Kubernetes**

The standard deployment uses Helm charts from the Aether project. The version of the Chart can be found in the OnRamp repository in the `vars/main.yml` file.


## Quick Navigation
| Goal                                      | Path / Directory                                               | Description                                                                |
| ----------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **View or modify configuration logic**    | [`factory/`](./factory)                                        | Handles NSSF configuration loading, initialization, and testing.           |
| **Understand slice selection behavior**   | [`nsselection/`](./nsselection)                                | APIs for selecting the appropriate network slice for UEs.                  |
| **Explore NSSAI availability management** | [`nssaiavailability/`](./nssaiavailability)                    | Implements slice availability tracking and subscriptions.                  |
| **Review main service startup**           | [`service/init.go`](./service/init.go), [`nssf.go`](./nssf.go) | Entry points for initializing and running the NSSF.                        |
| **Check NF registration with NRF**        | [`nfregistration/`](./nfregistration)                          | Manages NSSF registration and discovery procedures.                        |
| **Inspect producer logic**                | [`producer/`](./producer)                                      | Core NSSF procedures for responding to NF queries and managing slice data. |
| **Examine metrics and telemetry setup**   | [`metrics/`](./metrics)                                        | Monitors and exports telemetry data for performance insights.              |
| **Debug logs or change log level**        | [`logger/`](./logger)                                          | Centralized logging system configuration.                                  |
| **Review utility functions**              | [`util/`](./util)                                              | General helper and utility methods used across NSSF modules.               |
| **Run or build NSSF in Docker**           | [`Dockerfile`](./Dockerfile), [`Makefile`](./Makefile)         | Container and build definitions for deployment.                            |
| **Test and validate NSSF configuration**  | [`test/`](./test)                                              | Sample configurations and test files for functional validation.            |


## Reach out to us thorugh

1. #sdcore-dev channel in [ONF Community Slack](https://onf-community.slack.com/)
2. Raise Github issues
