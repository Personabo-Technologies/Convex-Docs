<div>

<div>

<div>

<div>

-   Home
-   Functions
-   Mutations

<div>

On this page

</div>

<div>

<div>

# Mutations

</div>

Mutations insert, update and remove data from the database, check
authentication or perform other business logic, and optionally return a
response to the client application.

## Mutation names​

The naming of Mutations follows the exact same rules as that of queries,
see Query names.

Queries and mutations can be defined in the same file when using named
exports.

## The `mutation` constructor​

To declare a mutation in Convex use the `mutation` constructor function,
and pass it an implementation function:

<div>

<div>

convex/doNothing.js

</div>

<div>

    import { mutation } from "./_generated/server";

    export default mutation(() => {
      // implementation will be here
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Mutation arguments and responses​

Just like for queries, named arguments passed to your mutation from a
client are accessible from the second parameter of the implementation
function:

<div>

<div>

convex/addAndSave.js

</div>

<div>

    import { mutation } from "./_generated/server";

    export default mutation((_, { a, b }) => {
      // do something with `a` and `b`
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Arguments are automatically serialized and deserialized, and you can
pass and return most value-like JavaScript data to and from your
function. See Field Values for the full list of supported types.

Unlike a query, a mutation does not have to return a value.

The first argument to the implementation function is reserved for the
mutation context.

### Mutation context​

The `mutation` constructor enables writing data to the database, and
other Convex features by passing a MutationCtx object to the
implementation function as the first argument:

<div>

<div>

convex/myMutation.js

</div>

<div>

    import { mutation } from "./_generated/server";

    export default mutation((mutationCtx, { a, b }) => {
      // Do something with `mutationCtx`
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Which part of the mutation context is used depends on what your mutation
needs to do:

-   To read from and write to the database use the `db` field. Note that
    we make the implementation function an `async` function so we can
    `await` the promise returned by `db.insert()`:

    <div>

    <div>

        export default mutation(async ({ db }, { name }) => {
          await db.insert("items", { name });
        });

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    Read on about Writing Data.

-   To generate upload URLs for storing files use the `storage` field.
    Read on about File Storage.

-   To check user authentication use the `auth` field. Read on about
    Authentication.

## Calling Mutations from Clients​

To call a Mutation from React use the generated `useMutation` hook:

<div>

<div>

src/MyApp.jsx

</div>

<div>

    import { useMutation } from "../convex/_generated/react";

    export function MyApp() {
      const mutateSomething = useMutation("mutateSomething");
      const handleClick = () => {
        mutateSomething({ a, b });
      };
      // pass `handleClick` to a button
      …

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

See Client Libraries for all the ways mutations can be called from
different clients.

## Transactions​

Mutations run **transactionally**. This means that:

1.  All database reads inside the transaction get a consistent view of
    the data in the database. You don\'t have to worry about a
    concurrent update changing the data in the middle of the execution.
2.  All database writes get committed together. If the Mutation writes
    some data to the database, but later throws an error, no data is
    actually written to the database.

For this to work, similarly to queries, mutations must be deterministic,
and cannot call third party APIs. To call third party APIs, use actions.

</div>

</div>

</div>

</div>

</div>
