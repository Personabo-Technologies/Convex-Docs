<div>

<div>

<div>

<div>

-   Home
-   Functions
-   Internal Functions

<div>

On this page

</div>

<div>

<div>

# Internal Functions

</div>

Internal functions can only be called by other functions, and cannot be
called directly from a Convex client.

## Defining internal functions​

An internal function is defined using `internalQuery`,
`internalMutation`, or `internalAction`. For example:

<div>

<div>

convex/markPlanAsProfessional.js

</div>

<div>

    import { internalMutation } from "./_generated/server";

    export default internalMutation(async ({ db }, { planId }) => {
      await db.patch(planId, { planType: "professional" });
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

<div>

<div>

convex/actions/upgrade.js

</div>

<div>

    import { action } from "../_generated/server";

    export default action(async ({ runMutation }, { planId, ... }) => {
      // Call out to payment provider (e.g. Stripe) to charge customer
      const response = await fetch(...);
      if (response.ok) {
        // Mark the plan as "professional" in the Convex DB
        await runMutation("markPlanAsProfessional", { planId });
      }
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

In this example a user should not be able to directly call
`markPlanAsProfessional` without going through the `upgrade` action ---
if they did, then they would get a free upgrade.

## Calling internal functions​

Leverage internal functions by:

-   Scheduling them from other functions to run in the future
-   Scheduling them to run periodically from cron jobs
-   Calling them from actions via `runQuery` and `runMutation`
-   Calling them from HTTP endpoints via `runQuery`, `runMutation`, and
    `runAction`
-   Testing them using the Dashboard

</div>

</div>

</div>

</div>

</div>
