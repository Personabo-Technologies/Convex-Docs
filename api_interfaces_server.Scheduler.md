<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   Scheduler

<div>

On this page

</div>

<div>

<div>

# Interface: Scheduler\<API\>

</div>

server.Scheduler

An interface to schedule Convex functions. The scheduled functions are
scheduled and executed only if the function that is scheduling them
completes successfully.

You can schedule either mutations or actions. Mutations are guaranteed
to execute exactly once - they are automatically retried on transient
errors and either execute successfully or fail deterministically due to
developer error in defining the function. Actions execute at most once -
they are not retried and might fail due to transient errors.

Consider using an internalMutation or internalAction to enforce that
these functions cannot be called directly from a Convex client.

## Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

## Methods​

### runAfter​

▸ **runAfter**\<`Name`\>(`delayMs`, `name`, `...args`):
`Promise`\<`void`\>

Schedule a function to execute after a delay.

#### Type parameters​

  Name     Type
  -------- ------------------
  `Name`   extends `string`

#### Parameters​

  Name        Type                                                                                                 Description
  ----------- ---------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `delayMs`   `number`                                                                                             delay in milliseconds. Must be non-negative. If the delay is zero, the scheduled function will be due to execute immediately after the scheduling one completes.
  `name`      `Name`                                                                                               the name of the function to schedule.
  `...args`   `Parameters`\<`NamedMutation`\<`API`, `Name`\>\> \| `Parameters`\<`NamedAction`\<`API`, `Name`\>\>   arguments to call the scheduled functions with.

#### Returns​

`Promise`\<`void`\>

------------------------------------------------------------------------

### runAt​

▸ **runAt**\<`Name`\>(`timestamp`, `name`, `...args`):
`Promise`\<`void`\>

Schedule a function to execute at a given timestamp.

#### Type parameters​

  Name     Type
  -------- ------------------
  `Name`   extends `string`

#### Parameters​

  Name          Type                                                                                                 Description
  ------------- ---------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `timestamp`   `number` \| `Date`                                                                                   a Date or a timestamp (milliseconds since the epoch). If the timestamp is in the past, the scheduled function will be due to execute immediately after the scheduling one completes. The timestamp can\'t be more than five years in the past or more than five years in the future.
  `name`        `Name`                                                                                               the name of the function to schedule.
  `...args`     `Parameters`\<`NamedMutation`\<`API`, `Name`\>\> \| `Parameters`\<`NamedAction`\<`API`, `Name`\>\>   arguments to call the scheduled functions with.

#### Returns​

`Promise`\<`void`\>

</div>

</div>

</div>

</div>

</div>
