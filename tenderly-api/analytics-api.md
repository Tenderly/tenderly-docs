# Analytics API

## API Authentication

You can read more about API authentication here: [Authenticating with the Tenderly API](authenticating-with-the-tenderly-api.md).

## Analytics API

The Analytics API provides a JSON query language that can be used to query over execution data indexed in Tenderly.

The analytics API indexes each block **after 10 confirmations**. The reason for this is of a technical nature: we didn't want to cache any results, impose restrictions how often a query can be ran etc. By waiting for 10 confirmations, we were able to index data in a more efficient way.

{% hint style="warning" %}
The data can be transformed, parsed and indexed in any way needed. As supporting such a generic API would be a huge undertaking, custom analytics requests can be sent to the Tenderly team. This way your team can get a custom API catering to your analytical needs.
{% endhint %}

## Project Slug

As all Tenderly resources are grouped inside of Projects, and a project slug must be provided in order to manage them.

You can find the project slug by calling the Project List endpoint.

```text
curl -X GET '<https://api.tenderly.co/api/v1/account/me/projects?withShared=true>' \\
--header "X-Access-Key: ${access_key}"
```

## Endpoints

**Production Endpoint**: `https://api.tenderly.co`

## Dashboards and Widgets

Analytics in Tenderly are stored in form of multiple dashboards, where each can dashboard can store multiple widgets.

![](../.gitbook/assets/image%20%2813%29.png)

{% hint style="info" %}
Widgets don't store the data itself, only the definition how to fetch the data. See the **Calculate** section on how to fetch data.
{% endhint %}

### Get Dashboards

**Method**: `GET`

**Endpoint**: `{{endpoint}}/api/v1/account/me/project/{{slug}}/analytics/dashboards`

**Request Payload**: N/A

**Response**:

```text
{
  "dashboards": [
    {
      "id": "e775bb37-b47f-4469-8777-6e4fdfd966aa",
      "project_id": "d55a5d1d-455f-494d-9b00-a43756109fef:uber-cool-project",
      "name": "Uber Cool Project Dashboard",
      "index": 0,
      "default_dashboard": true,
      "widget_ordering": [
        "0e687ce5-bc88-4186-a1cc-3f2077b8055a"
      ],
      "analytics_widgets": [
        {
          "id": "0e687ce5-bc88-4186-a1cc-3f2077b8055a",
          "analytics_dashboard_id": "e775bb37-b47f-4469-8777-6e4fdfd966aa",
          "name": "Top Function Calls",
          "analytics_table": "ethereum_transactions",
          "resolution": "day",
          "time_range": {
            "window": {
              "resolution": "day",
              "amount": 7
            }
          },
          "group_by": [
            "function_signature",
            "contract_to",
            "network_id"
          ],
          "order_by": [
            {
              "field": "address",
              "direction": "desc"
            }
          ],
          "selectors": [
            {
              "selector": {
                "aggregate": "count",
                "field": "address"
              }
            }
          ],
          "display_settings": {
            "chart_type": "table"
          },
          "filters": {},
          "default_widget": true
        }
      ],
      "created_at": "2020-03-02T12:29:41.123782Z"
    }
  ],
  "custom_dashboards": []
}
```

### Create Dashboard

**Method**: `POST`

**Endpoint**: `{{endpoint}}/api/v1/account/me/project/{{slug}}/analytics/dashboard`

**Request Payload**:

```text
{
  "name": "New Dashboard Name"
}
```

**Response**:

```text
{
  "dashboard": {...}
}
```

### Update Dashboard

**Method**: `PATCH`

**Endpoint**: `{{endpoint}}/api/v1/account/me/project/{{slug}}/analytics/dashboard/{{id}}`

**Request Payload**:

```text
{
  "name": "Updated Name",
  "index": {{index-of-the-dashboard}}
	"widget_ordering": [...]
}
```

**Response**:

```text
{
  "dashboard": {...}
}
```

### Delete Dashboard

**Method**: `DELETE`

**Endpoint**: `{{endpoint}}/api/v1/account/me/project/{{slug}}/analytics/dashboard/{{id}}`

**Request Payload**: N/A

**Response**: N/A

### Create Widget

**Method**: `POST`

**Endpoint**: `{{endpoint}}/api/v1/account/me/project/{{slug}}/analytics/dashboard/{{dashoard-id}}/widget`

**Request Payload**:

```text
{
  "dashboard_id": "e775bb37-b47f-4469-8777-6e4fdfd966aa",
  "name": "Gas Used New",
  "filters": {},
  "time_range": {...},
  "table": "{{table}}",
  "selectors": [...],
  "resolution": "{{resolution}}",
  "group_by": [...],
  "display_settings": {...}
}
```

You'll read more about the `name`, `filters`, `time_range`, `table`, `selectors`, `resolution`, `group_by` and `display_settings`

**Response**:

```text
{
  "widget": {
    "id": "e67a2f42-cf6d-4edd-9dbe-afb46660028a",
    "analytics_dashboard_id": "e775bb37-b47f-4469-8777-6e4fdfd966aa",
    "name": "Gas Used New"
    // ...
  }
}
```

### Update Widget

**Method**: `PATCH`

**Endpoint**: `{{endpoint}}/api/v1/account/me/project/{{slug}}/analytics/dashboard/{{dashoard-id}}/widget/{{widget-id}}`

**Request Payload**:

```text
{
  "dashboard_id": "e775bb37-b47f-4469-8777-6e4fdfd966aa",
  "name": "Gas Used New",
  "filters": {},
  "time_range": {...},
  "table": "{{table}}",
  "selectors": [...],
  "resolution": "{{resolution}}",
  "group_by": [...],
  "order_by": [...],
  "display_settings": {...}
}
```

You'll read more about the `name`, `filters`, `time_range`, `table`, `selectors`, `resolution`, `group_by` and `display_settings`

**Response**:

```text
{
  "widget": {
    "id": "e67a2f42-cf6d-4edd-9dbe-afb46660028a",
    "analytics_dashboard_id": "e775bb37-b47f-4469-8777-6e4fdfd966aa",
    "name": "Gas Used New"
    // ...
  }
}
```

### Delete Widget

**Method**: `DELETE`

**Endpoint**: `{{endpoint}}/api/v1/account/me/project/{{slug}}/analytics/dashboard/{{dashoard-id}}/widget/{{widget-id}}`

**Request Payload**: N/A

**Response**: N/A

## Calculate

The calculate endpoint is used as a generic endpoint for fetching analytical data that is indexed inside of Tenderly. Right now, via this API, you can query the transaction and the events datasets. For additional datasets, you'll need to contact the Tenderly team.

**Method**: `POST`

**Endpoint**: `{{endpoint}}/api/v1/account/me/project/{{slug}}/analytics/data?newFormat=true`

**Request Payload**:

```text
{
  "dashboard_id": "e775bb37-b47f-4469-8777-6e4fdfd966aa",
  "name": "{{name}}",
  "filters": {...},
  "time_range": {...},
  "table": "{{table}}",
  "selectors": [...],
  "resolution": "{{resolution}}",
  "display_settings": {...}
}
```

**Response**

```text
{
  "widget": {
    "call_count": {
      "resolution": "day",
      "time_range": {
        "window": {
          "resolution": "day",
          "amount": 7
        }
      },
      "group_by": [
        "contract_to"
      ],
      "order_by": [],
      "selectors": [
        {
          "predefined_selector": "call_count"
        }
      ],
      "display_settings": {
        "chart_type": "line_chart"
      },
      "data": {
        "0x06012C8CF97BEAD5DEAE237070F9587F8E7A266D": [
          [
            1611273600,
            133
          ],
          [
            1611360000,
            517
          ],
          [
            1611446400,
            429
          ],
          [
            1611532800,
            366
          ],
          [
            1611619200,
            406
          ],
          [
            1611705600,
            315
          ],
          [
            1611792000,
            490
          ],
          [
            1611878400,
            104
          ]
        ],
        "0x06AF07097C9EEB7FD685C692751D5C66DB49C215": [
          [
            1611273600,
            24
          ],
          [
            1611360000,
            5
          ],
          [
            1611446400,
            19
          ],
          [
            1611532800,
            7
          ],
          [
            1611619200,
            4
          ],
          [
            1611705600,
            16
          ],
          [
            1611792000,
            38
          ],
          [
            1611878400,
            1
          ]
        ],
        "0x0E3A2A1F2146D86A604ADC220B4967A898D7FE07": [
          [
            1611273600,
            20
          ],
          [
            1611360000,
            81
          ],
          [
            1611446400,
            16
          ],
          [
            1611532800,
            17
          ],
          [
            1611619200,
            39
          ],
          [
            1611705600,
            69
          ],
          [
            1611792000,
            41
          ],
          [
            1611878400,
            5
          ]
        ],
        "0x6B175474E89094C44DA98B954EEDEAC495271D0F": [
          [
            1611273600,
            28047
          ],
          [
            1611360000,
            66196
          ],
          [
            1611446400,
            73642
          ],
          [
            1611532800,
            70038
          ],
          [
            1611619200,
            58979
          ],
          [
            1611705600,
            56627
          ],
          [
            1611792000,
            51450
          ],
          [
            1611878400,
            22845
          ]
        ],
        "0x7FE3FE4B523D7F83DC05224573B01296877DC163": [
          [
            1611273600,
            25
          ],
          [
            1611360000,
            43
          ],
          [
            1611446400,
            44
          ],
          [
            1611532800,
            121
          ],
          [
            1611619200,
            115
          ],
          [
            1611705600,
            73
          ],
          [
            1611792000,
            19
          ],
          [
            1611878400,
            29
          ]
        ],
        "0x818E6FECD516ECC3849DAF6845E3EC868087B755": [
          [
            1611273600,
            51
          ],
          [
            1611360000,
            138
          ],
          [
            1611446400,
            150
          ],
          [
            1611532800,
            173
          ],
          [
            1611619200,
            171
          ],
          [
            1611705600,
            200
          ],
          [
            1611792000,
            124
          ],
          [
            1611878400,
            104
          ]
        ],
        "0x9F8F72AA9304C8B593D555F12EF6589CC3A579A2": [
          [
            1611273600,
            2717
          ],
          [
            1611360000,
            3905
          ],
          [
            1611446400,
            3948
          ],
          [
            1611532800,
            3020
          ],
          [
            1611619200,
            2928
          ],
          [
            1611705600,
            2354
          ],
          [
            1611792000,
            2865
          ],
          [
            1611878400,
            2064
          ]
        ]
      },
      "legend": {
        "items": {
          "0x06012C8CF97BEAD5DEAE237070F9587F8E7A266D": {
            "labels": {
              "Account": "KittyCore"
            }
          },
          "0x06AF07097C9EEB7FD685C692751D5C66DB49C215": {
            "labels": {
              "Account": "Chai"
            }
          },
          "0x0E3A2A1F2146D86A604ADC220B4967A898D7FE07": {
            "labels": {
              "Account": "BatchWrapper"
            }
          },
          "0x6B175474E89094C44DA98B954EEDEAC495271D0F": {
            "labels": {
              "Account": "Dai"
            }
          },
          "0x7FE3FE4B523D7F83DC05224573B01296877DC163": {
            "labels": {
              "Account": "KyberPriceFeed"
            }
          },
          "0x818E6FECD516ECC3849DAF6845E3EC868087B755": {
            "labels": {
              "Account": "KyberNetworkProxy"
            }
          },
          "0x9F8F72AA9304C8B593D555F12EF6589CC3A579A2": {
            "labels": {
              "Account": "DSToken"
            }
          }
        }
      }
    }
  }
}
```

### Analytics fields

There are multiple fields that can be used for querying, grouping, and ordering data. Some fields exist in both tables, while others are exclusive to a single table.

#### Fields in `ethereum_transactions` and `ethereum_transaction_logs`

* `address`
* `block_hash`
* `block_number`
* `transaction_index`
* `transaction_hash`

#### Fields in the `ethereum_transactions` table

* `transaction_status`
* `from`
* `to`
* `gas`
* `gas_price`
* `gas_used`
* `gas_used_total`
* `cumulative_gas_used`
* `function_signature`
* `value`
* `contract_address`

#### Fields in the `ethereum_transaction_logs` table

* `log_signature`

#### Virtual fields via predefined selectors

* `call_count`
* `tx_count`
* `tx_fee`

#### `table`

Can be either `ethereum_transactions` or `ethereum_transaction_logs` for the generic analytics endpoint.

The `ethereum_transactions` table contains all top level and internal transactions that ever happened. The `ethereum_transaction_logs` table contain all of the logs ever emitted.

#### `selectors`

An array of selectors, used for picking which part of the data set should be used and which aggregations should be applied. Selectors come in two variants: predefined selectors and normal selectors.

**Predefined selectors**

Predefined selectors ease the use of some of the fields that are present in the supported analytics tables.

```text
{
  "predefined_selector": "call_count/tx_count/tx_fee"
}
```

**Standard selectors**

Standard selector use aggregates to calculate analytical data. Supported aggregate functions are:

* `count`
* `sum`
* `avg`
* `median`
* `min`
* `max`
* `unique`

```text
{
  "field": "{{[field](<https://www.notion.so/Analytics-API-4ca952a1ea3442af838a5bd4fa2fbe0e>)}}",
  "aggregate": "{{aggregate}}"
}
```

#### `resolution`

Can be one of: `minute`, `hour`, `day`, `week`, `month`.

#### `time_range`

There are two types of time ranges supported: window and absolute. The window time range provides a relative way of querying the data, while the absolute one takes in concrete two dates.

**Window**

```text
{
  "window": {
    "resolution": "{{[resolution](<https://www.notion.so/Analytics-API-4ca952a1ea3442af838a5bd4fa2fbe0e>)}}",
    "amount": {{amount}}
  }
}
```

**Absolute**

```text
{
  "absolute": {
    "from": "{{from-iso-8601}}",
    "to": "{{to-iso-8601}}"
  }
}
```

#### `group_by`

An array of fields to use for grouping the aggregated results. In the UI this property is called **Breakdown**. Can be one of:

* `network_id`: The network on which the address is
* `contract_from`: The `from` address of an \(internal\) transaction
* `contract_to`: The `to` address of an \(internal\) transaction
* `function_signature`: The function selector of a particular \(internal\) call
* `transaction_status`: Whether the \(internal\) call was successful or not
* `log_signature`: The `topic[0]` of an emitted log
* `contract_address`: The address of the contract that emitted a particular log

#### `order_by`

An array of field and direction pairs, used for sorting the result set

```text
[
  {
    "field": "{{[field](<https://www.notion.so/Analytics-API-4ca952a1ea3442af838a5bd4fa2fbe0e>)}}",
    "direction": "asc/desc"
  }
]
```

#### `display_settings`

The data returned by the analytics API can be pre-transformed for specific chart types:

* `line_chart`
* `stacked_line_chart`
* `table`
* `bar_chart`
* `stacked_bar_chart`
* `gauge_chart`

```text
{
  "chart_type": "{{chart_type}}"
}
```

#### `filters`

There are three ways to filter addresses inside of the project when calculating analytics. Multiple filters can be combined.

**Contract IDs**

Even thought the name suggests only contacts are support, EOA accounts are supported as well. The IDs follow the format `eth:{{network_id}}:{{lowercase_address}}`.

```text
{
  "contracts_ids": [...]
}
```

**Network IDs**

An array of Ethereum Network IDs.

```text
{
  "network_ids": [...]
}
```

**Tags**

An array of tags that were previously added to the addresses in of the project.

```text
{
  "tags": [...]
}
```

