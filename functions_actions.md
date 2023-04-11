<div>

<div>

<div>

<div>

-   Home
-   Functions
-   Actions

<div>

On this page

</div>

<div>

<div>

# Actions

</div>

**Example:** GIPHY Action

Actions can call third party services to do things such as processing a
payment with Stripe. They can execute any JavaScript code and use any
Node package as a dependency. They can interact with the database
indirectly by calling queries and mutations.

## Action names​

Actions are defined in files inside the `convex/actions/` directory.

They follow the same naming rules as queries, but their name always
starts with the `"actions/"` prefix:

<div>

<div>

convex/actions/myAction.js

</div>

<div>

    // This action will be named "actions/myAction".
    export default …;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## The `action` constructor​

To declare an action in Convex you use the action constructor function
and pass it an implementation function:

<div>

<div>

convex/actions/myAction.js

</div>

<div>

    import { query } from "./_generated/server";

    export default action(() => {
      // implementation goes here
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Action arguments and responses​

Action arguments and responses follow the same rules as mutations:

<div>

<div>

convex/actions/myAction.js

</div>

<div>

    import { action } from "./_generated/server";

    export default action((_, { a, b }) => {
      // do something with `a` and `b`
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

The first argument to the implementation function is reserved for the
action context.

## Action context​

The `action` constructor enables interacting with the database, and
other Convex features by passing an ActionCtx object to the
implementation function as the first argument:

<div>

<div>

convex/actions/myAction.js

</div>

<div>

    import { action } from "./_generated/server";

    export default action((actionCtx, { a, b }) => {
      // Do something with `actionCtx`
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Which part of that action context is used depends on what your Action
needs to do:

-   To read data from the database use the `runQuery` field, and call a
    query that performs the read:

    <div>

    <div>

    convex/actions/myAction.js

    </div>

    <div>

        export default action(async ({ runQuery }, { a, b }) => {
          const data = await runQuery("readData", { a });
          // do something with `data`
        });

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    Use an internal query when you want to prevent users from calling
    the query directly.

-   To write data to the database use the `runMutation` field, and call
    a mutation that performs the write:

    <div>

    <div>

    convex/actions/myAction.js

    </div>

    <div>

        export default action(async ({ runMutation }, { a, b }) => {
          await runMutation("writeData", { a });
          // do something else
        });

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    Use an internal mutation when you want to prevent users from calling
    the mutation directly.

-   To check user authentication use the `auth` field. Auth is
    propagated automatically when calling queries and mutations from the
    action. Read on about Authentication.

## Calling third-party APIs​

You can use any Node.js package in actions, including libraries that
make requests to third party services. To use `fetch` you\'ll need the
`node-fetch` library because actions run under Node.js 16 where native
`fetch` is not available.

<div>

<div>

convex/actions/myAction.js

</div>

<div>

    import { action } from "./_generated/server";
    import fetch from "node-fetch";

    export default action(async _ => {
      const data = await fetch("https://api.thirdpartyservice.com");
      // do something with data
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Calling Actions from Clients​

To call an action from React use the generated `useAction` hook:

<div>

<div>

src/MyApp.jsx

</div>

<div>

    import { useAction } from "../convex/_generated/react";

    export function MyApp() {
      const performSomeAction = useAction("someActionName");
      const handleClick = () => {
        performSomeAction({ a, b });
      };
      // pass `handleClick` to a button
      …

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

See Client Libraries for all the ways Actions can be called from
different clients.

## Resource Limits​

Actions time out after 2 minutes and they can use up to 512MB of memory.
Please contact us if you have a use case that requires higher limits.

## Error handling​

Unlike Queries and Mutations, actions may have side-effects and
therefore can\'t be automatically retried by Convex when errors occur.
For example, say your action calls Stripe to send a customer invoice. If
the HTTP request fails, Convex has no way of knowing if the invoice was
already sent. Like in normal backend code, it is the responsibility of
the caller to handle errors raised by actions and retry the action call
if appropriate.

Make sure to await all promises created within an action. Async tasks
still running when the function returns might or might not complete. In
addition, since the Node.js execution environment might be reused
between action calls, dangling promises might result in errors in
subsequent action invocations.

</div>

</div>

</div>

</div>

</div>
