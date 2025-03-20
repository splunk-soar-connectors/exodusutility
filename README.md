# Exodus

Publisher: Mhike \
Connector Version: 1.0.1 \
Product Vendor: Mhike \
Product Name: Exodus \
Minimum Product Version: 4.9.0

The Exodus app manages various operations used in migrating content from dev to prod

### Configuration variables

This table lists the configuration variables required to operate Exodus. These variables are specified when configuring a Exodus asset in Splunk SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**source_base_url** | required | string | URL for source SOAR host |
**source_api_token** | required | password | API token for source SOAR host |
**source_dev_repo_id** | required | string | Dev Repository ID for source SOAR host |
**source_prod_repo_id** | optional | string | Prod repository ID on source SOAR host |
**source_tenant_id** | optional | string | Tenant ID on source SOAR host |
**target_base_url** | required | string | URL for target SOAR host |
**target_api_token** | required | password | API token for target SOAR host |
**target_repo_id** | required | string | Prod repository ID on target SOAR host |
**debug** | optional | boolean | Print debugging statements to log |

### Supported Actions

[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied credentials \
[add approval](#action-add-approval) - Add approval artifact to container \
[on poll](#action-on-poll) - Execute migration options

## action: 'test connectivity'

Validate the asset configuration for connectivity using supplied credentials

Type: **test** \
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

## action: 'add approval'

Add approval artifact to container

Type: **generic** \
Read only: **False**

Add a specifically formatted artifact that is required for the approval process for exodus containers.

#### Action Parameters

No parameters are required for this action

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.data | string | | |
action_result.summary | string | | |
action_result.message | string | | |
summary.total_objects | numeric | | |
summary.total_objects_successful | numeric | | |

## action: 'on poll'

Execute migration options

Type: **ingest** \
Read only: **False**

Create required exodus containers and migrate approved content to production system.

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

______________________________________________________________________

Auto-generated Splunk SOAR Connector documentation.

Copyright 2025 Splunk Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
