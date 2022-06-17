# Diagrams

## Full Diagram

```mermaid
  graph LR
  WorkflowModel-->Auth
  WorkflowModel-->Constants
  WorkflowModel-->DataInputSchema
  WorkflowModel-->Errors
  WorkflowModel-->Events
  WorkflowModel-->Extension
  WorkflowModel-->Functions
  WorkflowModel-->Retries
  WorkflowModel-->Secrets
  WorkflowModel-->Start
  WorkflowModel-->State
  WorkflowModel-->TimeoutsDefinition
  
  Auth-->AuthDefinition
  
  AuthDefinition-->BasicAuthDefinition
  AuthDefinition-->BearerAuthDefinition
  AuthDefinition-->OauthDefinition
 
  Functions-->FunctionDefinition
  
  Events-->EventDefinition
  
  Retries-->RetryDefinition
  
  Start-->Schedule
  
  Schedule-->Cron
  
  EventDefinition-->CorrelationDefinition
  
  TimeoutsDefinition-->StateExecTimeout
  TimeoutsDefinition-->WorkflowExecTimeout
  
  Errors-->ErrorDefinition
  
  State-->End
  State-->Error
  State-->StateDataFilter
  State-->TimeoutsDefinition
  State-->Transition
  
  State-->EventState
  State-->OperationState
  State-->SwitchState
  State-->SleepState
  State-->ParallelState
  State-->InjectState
  State-->ForEachState
  State-->CallbackState
  
  EventState-->OnEvents
  
  OperationState-->Action
  
  SwitchState-->DataCondition
  SwitchState-->DefaultConditionDefinition
  SwitchState-->EventCondition
  
  ParallelState-->Branch
  
  ForEachState-->Action
  
  CallbackState-->Action
  CallbackState-->EventDataFilter
  
  Branch-->Action
  Branch-->TimeoutsDefinition
  
  EventCondition-->End
  EventCondition-->EventDataFilter
  EventCondition-->Transition
  
  DefaultConditionDefinition-->End
  DefaultConditionDefinition-->Transition
  
  DataCondition-->End
  DataCondition-->Transition
  
  OnEvents-->Action
  OnEvents-->EventDataFilter
  
  Action-->ActionDataFilter
  Action-->EventRef
  Action-->FunctionRef
  Action-->Sleep
  Action-->SubFlowRef
  
  Transition-->ProduceEvent
  
  Error-->End
  
  End-->ContinueAs
  End-->ProduceEvent
  
  ContinueAs-->WorkflowExecTimeout
```

## WorkflowModel

```mermaid
  graph TD
  
  WorkflowModel-->Auth
  WorkflowModel-->Constants
  WorkflowModel-->DataInputSchema
  WorkflowModel-->Events
  WorkflowModel-->Extension
  WorkflowModel-->Functions
  WorkflowModel-->Retries
  WorkflowModel-->Secrets
  
  WorkflowModel-->RetryDefinition
  WorkflowModel-->TimeoutsDefinition
  WorkflowModel-->Errors
  WorkflowModel-->State
  WorkflowModel-->Start
```

## ParallelState
```mermaid
  graph LR
  WorkflowModel-->State-->ParallelState
```

## DataCondition

```mermaid
  graph LR
  WorkflowModel-->State-->SwitchState-->DataCondition
```

## Branch
```mermaid
  graph LR
  WorkflowModel-->State-->ParallelState-->Branch
```

## OnEvents
```mermaid
  graph LR
  WorkflowModel-->State-->EventState-->OnEvents
```

## Action

```mermaid
  graph LR
  WorkflowModel-->State
  State-->OperationState
  State-->ForEachState
  State-->CallbackState
  State-->ParallelState
  State-->EventState
  
  OperationState-->Action
  
  ForEachState-->Action
  
  CallbackState-->Action
  
  Branch-->Action
  
  ParallelState-->Branch
  
  OnEvents-->Action
  
  EventState-->OnEvents
```

## EventCondition
```mermaid
  graph LR
  WorkflowModel-->State-->SwitchState-->EventCondition
```

## DefaultConditionDefinition
```mermaid
  graph LR
  WorkflowModel-->State-->SwitchState-->DefaultConditionDefinition
```

## Transition
```mermaid
  graph LR
  WorkflowModel-->State-->SwitchState-->DataCondition-->Transition
  State-->Transition
  SwitchState-->EventCondition-->Transition
  SwitchState-->DefaultConditionDefinition-->Transition
```

## EventRef
```mermaid
  graph LR
  WorkflowModel-->State
  State-->OperationState-->Action
  State-->ForEachState-->Action
  State-->CallbackState-->Action
  State-->ParallelState-->Branch-->Action
  State-->EventState-->OnEvents-->Action
  Action-->EventRef
```

## Error
```mermaid
  graph LR
  
  WorkflowModel-->State-->Error
```

## End
```mermaid
  graph LR
  
  WorkflowModel-->State
  State-->End
  State-->SwitchState
  State-->Error
  SwitchState-->DefaultConditionDefinition
  SwitchState-->DataCondition
  DefaultConditionDefinition-->End
  DataCondition-->End
  Error-->End
```

## ProduceEvent
```mermaid
  graph LR
  
  WorkflowModel-->State
  State-->SwitchState
  State-->Transition
  State-->End
  State-->Error
  SwitchState-->DataCondition
  SwitchState-->DefaultConditionDefinition
  SwitchState-->EventCondition
  Transition-->ProduceEvent
  DefaultConditionDefinition-->Transition
  DefaultConditionDefinition-->End
  EventCondition-->Transition
  DataCondition-->Transition
  DataCondition-->End
  Error-->End
  End-->ProduceEvent
```

## FunctionRef
```mermaid
  graph LR
  
  WorkflowModel-->State
  State-->OperationState
  State-->ForEachState
  State-->CallbackState
  State-->ParallelState
  State-->EventState
  
  OperationState-->Action
  
  ForEachState-->Action
  
  CallbackState-->Action
  
  Branch-->Action
  
  ParallelState-->Branch
  
  OnEvents-->Action
  
  EventState-->OnEvents

  Action-->FunctionRef
```