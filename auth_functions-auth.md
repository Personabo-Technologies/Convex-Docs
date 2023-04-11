<div>

<div>

<div>

<div>

-   Home
-   Authentication
-   Functions

<div>

On this page

</div>

<div>

<div>

# Auth in Functions

</div>

Within a Convex function, you can access information about the currently
logged-in user by using the the `auth` property of the `QueryCtx`,
`MutationCtx`, or `ActionCtx` object:

<div>

<div>

convex/myMutation.js

</div>

<div>

    import { mutation } from "../_generated/server";

    export default mutation(async ({ db, auth }) => {
      const identity = await auth.getUserIdentity();
      if (identity == null) {
        throw new Error("Unauthenticated call to mutation");
      }
      //...
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## User identity fields​

The UserIdentity object returned by `getUserIdentity` is guaranteed to
have `tokenIdentifier` and `issuer` fields. Which other fields it will
include depends on the identity provider used and the configuration of
JWT tokens and OpenID scopes.

If you followed one of our integrations with Clerk or Auth0 at least the
following fields will be present: `family_name`, `given_name`,
`nickname`, `picture`, `updated_at`, `email`, `email_verified`. See
their standard definition in the OpenID docs.

<div>

<div>

convex/myMutation.js

</div>

<div>

    export default mutation(async ({ db, auth }) => {
      const identity = await auth.getUserIdentity();
      const { tokenIdentifier, name, email } = identity;
      //...
    });

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
