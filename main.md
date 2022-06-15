# Workflow Validations

| Description                               | Implemented       |
|-------------------------------------------|-------------------|
| `id` is required if `key` is not defined. | Outdated          |
| `key` is required if `id` is not defined. | No                |
| `start` must refer to an existing `state` | Yes               |
| `states` is required                      | Manual and schema |
| `specVersion` is required.                | No                |

## States

| Description                                       | Implemented       |
|---------------------------------------------------|-------------------|
| `name` is required.                               | Manual and schema |
| `type` is required.                               | Schema            |
| `transition` is required if `end` is not defined  | No                |
| `transition` or `end` should be defined. Not both | No                |
| `transition` must refer to an existing `state`    | Yes               |
| `compensatedBy` must refer to an existing `state` | Yes               |

## OnEvents Definition

| Description                                   | Implemented |
|-----------------------------------------------|-------------|
| `eventRefs` is required                       | Schema      |
| `eventRefs` must refer to an existing `event` | Yes         |
| `actionMode` must be `sequence` or `parallel` | Schema      |

### States Referenced by `compensatedBy`

| Description                                                                                           | Implemented |
|-------------------------------------------------------------------------------------------------------|-------------|
| should not have any incoming transitions (should not be part of the main workflow control-flow logic) | No          |
| Cannot be an event state                                                                              | No          |
| Must define the `usedForCompensation` property and set it to `true`                                   | No          |
| Can transition only to states which also have their `usedForCompensation` property and set to `true`  | No          |
| Cannot themselves set their `compensatedBy` property (compensation is not recursive)                  | No          |

### Event State

| Description                                       | Implemented       |
|---------------------------------------------------|-------------------|
| `onEvents` is required                            | Manual and schema |

### Switch State

| Description                                                    | Implemented                                                    |
|----------------------------------------------------------------|----------------------------------------------------------------|
| `dataCondition` or `eventCondition` is required                | Yes                                                            |
| Both `dataCondition` and `eventCondition` must not be present. | Yes                                                            |
| `defaultCondition` is required.                                | Manual. Schema has an error (`default` is defined as required) |

#### Data Condition

| Description                                       | Implemented       |
|---------------------------------------------------|-------------------|
| `condition` is required                           | Manual and schema |
| `transition` or `end` is required                 | Schema            |
| `transition` or `end` should be defined. Not both | Schema            |
| `transition` must refer to an existing `state`    | Yes               |

#### Default Condition

| Description                                     | Implemented |
|-------------------------------------------------|-------------|
| `transition` or `end` is required               | Schema      |
| `transition` must refer to an existing `state`. | Yes         |

#### Event Condition

| Description                                       | Implemented         |
|---------------------------------------------------|---------------------|
| `eventRef` is required                            | Schema              |
| `eventRef` must refer to an existing `event`      | Yes                 |
| `transition` or `end` is required                 | Schema has an error |
| `transition` or `end` should be defined. Not both | Schema has an error |
| `transition` must refer to an existing `state`    | Yes                 |

### Sleep State

| Description                                            | Implemented |
|--------------------------------------------------------|-------------|
| `duration` is required                                 | Schema      |
| `duration` must be in a valid ISO 8601 duration format | No          |

### Operation State

| Description           | Implemented |
|-----------------------|-------------|
| `actions` is required | Schema      |

### Parallel State

| Description                                               | Implemented |
|-----------------------------------------------------------|-------------|
| `branches` is required                                    | Schema      |
| `completionType` must be `allOff` or `atLeast`            | Schema      |
| `numCompleted` is required if `completionType` is defined | No          |

#### Branch

| Description           | Implemented         |
|-----------------------|---------------------|
| `name` is required    | Schema              |
| `actions` is required | Schema has an error |

### Inject State

| Description        | Implemented         |
|--------------------|---------------------|
| `data` is required | Schema has an error |

### ForEach State

| Description                               | Implemented         |
|-------------------------------------------|---------------------|
| `inputCollection` is required             | Schema and Manual   |
| `actions` is required                     | Schema has an error |
| `mode` must be `sequential` or `parallel` | Schema              |

### Callback State

| Description                                  | Implemented |
|----------------------------------------------|-------------|
| `action` is required                         | No          |
| `eventRef` is required                       | No          |
| `eventRef` must refer to an existing `event` | Yes         |

## Function Definition

| Description                                                                             | Implemented |
|-----------------------------------------------------------------------------------------|-------------|
| `name` is required                                                                      | Schema      |
| `operation` is required                                                                 | No          |
| `type` must be `rest`, `asyncapi`, `rpc`, `graphql`, `odata`, `expression`, or `custom` | Schema      |
| `authRef` must refer to an existing `auth`                                              | Yes         |

### Operation

| Function Type | Valid Value                                                                        | Implemented |
|---------------|------------------------------------------------------------------------------------|-------------|
| `rest`        | <path_to_openapi_definition>#<operation_id>                                        | No          |
| `asyncapi`    | <path_to_asyncapi_definition>#<operation_id>                                       | No          |
| `rpc`         | <path_to_grpc_proto_file>#<service_name>#<service_method>                          | No          |
| `graphql`     | <url_to_graphql_endpoint>#<literal `mutation` or `query`>#<query_or_mutation_name> | No          |
| `odata`       | <URI_to_odata_service>#<Entity_Set_Name>                                           | No          |
| `expression`  | An expression                                                                      | No          |

## Event Definition

| Description                                         | Implemented |
|-----------------------------------------------------|-------------|
| `name` is required                                  | Schema      |
| `type` is required                                  | Schema      |
| `source` is required if `kind` is set to `consumed` | Schema      |
 | `kind` must be `consumed` or `produced`             | Schema      |

## Auth Definition

| Description                                     | Implemented |
|-------------------------------------------------|-------------|
| `name` is required                              | No          |
| `scheme` is required                            | No          |
| `scheme` must be `basic`, `bearer`, or `oauth2` | Schema      |
| `properties` is required                        | No          |

### Basic Properties Definition

| Description            | Implemented |
|------------------------|-------------|
| `username` is required | Schema      |
| `password` is required | Schema      |

### Bearer Properties Definition

| Description         | Implemented |
|---------------------|-------------|
| `token` is required | Schema      |

### OAuth2 Properties Definition

| Description                                                             | Implemented |
|-------------------------------------------------------------------------|-------------|
| `grantType` is required                                                 | Schema      |
| `grantType` must be `password`, `clientCredentials`, or `tokenExchange` | Schema      |
| `clientId` is required                                                  | Schema      |

## Correlation Definition

| Description                        | Implemented |
|------------------------------------|-------------|
| `contextAttributeName` is required | Schema      |

## Action Definition

| Description                                                              | Implemented                |
|--------------------------------------------------------------------------|----------------------------|
| `functionRef` is required if `eventRef` and `subFlowRef` are not defined | Schema OK. Manual Outdated |
| `eventRef` is required if `functionRef` and `subFlowRef` are not defined | Schema                     |
| `subFlowRef` is required if `eventRef` and `functionRef` are not defined | Schema                     |

### EventRef Definition

| Description                                              | Implemented |
|----------------------------------------------------------|-------------|
| `produceEventRef` is required                            | No          |
| `produceEventRef` must refer to an existing `event`      | No          |
| `consumeEventTimeout` must be in a valid ISO 8601 format | No          |
| `invoke` must be `sync` or `async`                       | No          |

## FunctionRef Definition

| Description                                              | Implemented |
|----------------------------------------------------------|-------------|
| `refName` is required                                    | Schema      |
| `refName` must refer to an existing `function`           | No          |
| `arguments` is required if function type is `graphql`    | No          |
| `selectionSet` is required if function type is `graphql` | No          |
| `invoke` must be `sync` or `async`                       | Schema      |

## SubFlowRef Definition

| Description                                          | Implemented |
|------------------------------------------------------|-------------|
| `workflowId` is required                             | Schema      |
| `invoke` must be `sync` or `async`                   | Schema      |
| `onParentComplete` must be `terminate` or `continue` | Schema      |

## Error Definition

| Description                                       | Implemented         |
|---------------------------------------------------|---------------------|
| `errorRef` or `errorRefs` is required             | Schema has an error |
| `transition` or `end` is required                 | Schema has an error |
| `transition` or `end` should be defined. Not both | Schema has an error |
| `transition` must refer to an existing `state`    | Yes                 |

## Retry Definition

| Description                                             | Implemented |
|---------------------------------------------------------|-------------|
| `name` is required                                      | Schema      |
| `delay` must be in a valid ISO 8601 duration format     | No          |
| `maxDelay` must be in a valid ISO 8601 duration format  | No          |
| `increment` must be in a valid ISO 8601 duration format | No          |

## Transition Definition

| Description                                   | Implemented |
|-----------------------------------------------|-------------|
| `nextState` is required                       | Schema      |
| `nextState` must refer to an existing `state` | Yes         |

## Start Definition

| Description                                   | Implemented |
|-----------------------------------------------|-------------|
| `stateName` must refer to an existing `state` | Yes         |
| `schedule` is required                        | No          |

## Schedule Definition

| Description                                     | Implemented |
|-------------------------------------------------|-------------|
| `interval` is required if `cron` is not defined | Schema      |
| `cron` is required if `interval` is not defined | Schema      |

## Cron Definition

| Description                                            | Implemented |
|--------------------------------------------------------|-------------|
| `expression` is required                               | Schema      |
| `validUnitl` must be a date and time (ISO 8601 format) | No          |

## Timeout Definition

| Description                                                                    | Implemented |
|--------------------------------------------------------------------------------|-------------|
| `workflowExecTimeout` must be a valid ISO 8601 duration if a string is defined | No          |
| `stateExecTimeout` must be a valid ISO 8601 duration if a string is defined    | No          |
| `actionExecTimeout` must be a valid ISO 8601 duration                          | No          |
| `branchExecTimeout` must be a valid ISO 8601 duration                          | No          |
| `eventTimeout` must be a valid ISO 8601 duration                               | Yes         |

### WorkflowExecTimeout Definition

| Description                                  | Implemented |
|----------------------------------------------|-------------|
| `duration` is required                       | Schema      |
| `duration` must be a valid ISO 8601 duration | No          |

## End Definition

### continueAs Definition

| Description              | Implemented |
|--------------------------|-------------|
| `workflowId` is required | No          |

### producedEvent Definition

| Description                                  | Implemented |
|----------------------------------------------|-------------|
| `eventRef` is required                       | Schema      |
| `eventRef` must refer to an existing `event` | Yes         |