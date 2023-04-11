<div>

<div>

<div>

<div>

-   Home
-   Functions
-   Queries

<div>

On this page

</div>

<div>

<div>

# Queries

</div>

Queries are the bread and butter of your backend API. They fetch data
from the database, check authentication or perform other business logic,
and return data back to the client application.

## Query names​

Queries are defined in files inside your `convex/` directory.

The path and name of the file, as well as the way the function is
exported from the file, determine the name the client will use to call
it.

The simplest name is given to functions `default export`ed from a file
placed directly in the `convex/` directory:

<div>

<div>

convex/myQuery.js

</div>

<div>

    // This function will be named "myQuery".
    export default …;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

To structure your API you can nest directories inside the `convex/`
directory:

<div>

<div>

convex/foo/myQuery.js

</div>

<div>

    // This function will be named "foo/myQuery".
    export default …;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Finally it can be handy to declare multiple functions in the same file.
This can be done with named exports:

<div>

<div>

convex/myFunctions.js

</div>

<div>

    // This function will be named "myFunctions:all".
    export const all = …;
    // This function will be named "myFunctions:some".
    export const some = …;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

You can mix and match all of these ways of naming your functions. The
same rules apply to mutations and actions, while HTTP endpoints use a
different routing approach.

## The `query` constructor​

To actually declare a query in Convex you use the `query` constructor
function, and pass it an implementation function returning the result:

<div>

<div>

convex/staticString.js

</div>

<div>

    import { query } from "./_generated/server";

    export default query(() => {
      return "My never changing string";
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Query arguments and responses​

Named arguments passed to your query from a client are accessible from
the second parameter of the implementation function:

<div>

<div>

convex/add.js

</div>

<div>

    import { query } from "./_generated/server";

    export default query((_, { a, b }) => {
      return a + b;
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Arguments are automatically serialized and deserialized, and you can
pass and return most value-like JavaScript data to and from your
function. See Field Values for the full list of supported types.

The first argument to the implementation function is reserved for the
query context.

### Query context​

The `query` constructor enables fetching data, and other Convex features
by passing a QueryCtx object to the implementation function as the first
argument:

<div>

<div>

convex/myQuery.js

</div>

<div>

    import { query } from "./_generated/server";

    export default query((queryCtx, { a, b }) => {
      // Do something with `queryCtx`
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Which part of the query context is used depends on what your query needs
to do:

-   To fetch from the database use the `db` field. Note that we make the
    implementation function an `async` function so we can `await` the
    promise returned by `db.get()`:

    <div>

    <div>

        export default query(async ({ db }, { id }) => {
          return await db.get(id);
        });

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    Read more about Reading Data.

-   To return URLs to stored files use the `storage` field. Read more
    about File Storage.

-   To check user authentication use the `auth` field. Read more about
    Authentication.

## Calling queries from clients​

To call a query from React use the generated `useQuery` hook:

<div>

<div>

src/MyApp.jsx

</div>

<div>

    import { useQuery } from "../convex/_generated/react";

    export function MyApp() {
      const data = useQuery("functionName", { a, b });
      …

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

See Client Libraries for all the ways queries can be called from
different clients.

## Caching & reactivity​

Queries have two awesome attributes:

1.  **Caching**: Convex caches query results automatically. If many
    clients request the same query, with the same arguments, they will
    receive a cached response.
2.  **Reactivity**: clients can subscribe to queries to receive new
    results when the underlying data changes.

To have these attributes the implementation function must be
*deterministic*, which means that given the same arguments (including
the query context) it will return the same response.

For this reason queries cannot call third party APIs. To call third
party APIs, use actions.

You might wonder whether you can use non-deterministic language
functionality like `Math.random()` or `Date.now()`. The short answer is
that Convex takes care of implementing these in a way that you don\'t
have to think about the deterministic constraint.

</div>

</div>

</div>

</div>

</div>
