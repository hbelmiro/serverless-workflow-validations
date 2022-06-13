# Diagrams

## Full Diagram

```mermaid
  graph LR
  WorkflowModel-->FunctionDefinition
  WorkflowModel-->EventDefinition
  WorkflowModel-->RetryDefinition
  WorkflowModel-->TimeoutsDefinition
  WorkflowModel-->Errors
  WorkflowModel-->State
  
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
  State-->OperationState-->Action
  State-->ForEachState-->Action
  State-->CallbackState-->Action
  State-->ParallelState-->Branch-->Action
  State-->EventState-->OnEvents-->Action
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