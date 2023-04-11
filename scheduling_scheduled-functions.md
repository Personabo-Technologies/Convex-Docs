<div>

<div>

<div>

<div>

-   Home
-   Scheduling
-   Scheduled Functions

<div>

On this page

</div>

<div>

<div>

# Scheduled Functions

</div>

**Example:** Scheduling

Convex allows you to schedule functions to run in the future. This
allows you to build powerful workflows without the need to setup and
maintain queues or other infrastructure.

## Scheduling functions​

You can schedule public functions and internal functions from mutations
and actions via the scheduler provided in the respective function
context.

-   runAfter schedules a function to run after a delay (measured in
    milliseconds).
-   runAt schedules a function run at a date or timestamp (measured in
    milliseconds elapsed since the epoch).

The rest of the arguments are the path to the function and its
arguments, similar to invoking a function from the client. For example,
here is how to send a message that self-destructs in five seconds.

<div>

<div>

convex/sendExpiringMessage.js

</div>

<div>

    import { mutation, internalMutation } from "./_generated/server";

    export default mutation(async ({ db, scheduler }, { body, author }) => {
      const id = await db.insert("messages", { body, author });
      await scheduler.runAfter(5000, "sendExpiringMessage:destruct", { id });
    });

    export const destruct = internalMutation(async ({ db }, messageId) => {
      await db.delete(messageId);
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

A single function can schedule up to 1000 functions with total argument
size of 8MB.

## Scheduling from mutations​

Scheduling functions from mutations is atomic with the rest of the
mutation. This means that if the mutation succeeds, the scheduled
function is guaranteed to be scheduled. On the other hand, if the
mutations fails, no function will be scheduled, even if the function
fails after the scheduling call.

## Scheduling from actions​

Unlike mutations, actions don\'t execute as a single database
transaction and can have side effects. Thus, scheduling from actions
does not depend on the outcome of function. This means that an action
might succeed to schedule some functions and later fail due to transient
error or a timeout. The scheduled functions will still be executed.

## Debugging​

You can view logs from previously executed scheduled functions in the
Convex dashboard Logs view. You can view and cancel yet to be executed
functions in the Functions view.

## Error handling​

Once scheduled, mutations are guaranteed to be executed exactly once.
Convex will automatically retry any internal Convex errors, and only
fail on developer errors. See Error Handling for more details on
different error types.

Since actions may have side effects, they are not automatically retried
by Convex. Thus, actions will be executed at most once, and permanently
fail if there are transient errors while executing them. Developers can
retry those manually by scheduling a mutation that checks if the desired
outcome has been achieved and if not schedule the action again.

## Auth​

The auth is not propagated from the scheduling to the scheduled
function. If you want to authenticate or check authorization, you\'ll
have to pass the requisite user information in as a parameter.

</div>

</div>

</div>

</div>

</div>
