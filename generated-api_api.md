<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Generated Code
-   api.d.ts

<div>

On this page

</div>

<div>

<div>

# api.d.ts

</div>

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)This code
is generated

</div>

<div>

These exports are not directly available in the `convex` package!

Instead you must run `npx convex codegen` to create
`convex/_generated/api.js` and `convex/_generated/api.d.ts`.

</div>

</div>

These types require running code generation because they are specific to
the Convex functions you define for your app.

If you aren\'t using code generation, you can use the generic version
instead, GenericAPI.

## Types​

### ConvexAPI​

Ƭ **ConvexAPI**: `Object`

A TypeScript type describing your app\'s public Convex API.

This `ConvexAPI` type includes information about the arguments and
return types of your app\'s Convex functions.

This type should be used with type-parameterized classes like
`ConvexReactClient` and `ConvexHttpClient` to create app-specific types.

<div>

<div>

    import { ConvexReactClient } from "convex/react";
    import { ConvexAPI } from "../convex/_generated/api";

    // typically loaded from an environment variable
    const address = "https://small-mouse-123.convex.cloud";
    const convex = new ConvexReactClient(address);

    const convex: ConvexReactClient<ConvexAPI> = new ConvexReactClient(address);

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>
