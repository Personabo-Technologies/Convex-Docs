<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Generated Code
-   react.js

<div>

On this page

</div>

<div>

<div>

# react.js

</div>

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)This code
is generated

</div>

<div>

These exports are not directly available in the `convex` package!

Instead you must run `npx convex codegen` to create
`convex/_generated/react.js` and `convex/_generated/react.d.ts`.

</div>

</div>

These hooks and types require running code generation because they
contain types specific to the Convex functions you define for your app.

If you aren\'t using code generation, you can use the generic versions
instead:

-   useQueryGeneric
-   useMutationGeneric
-   useActionGeneric
-   useConvexGeneric
-   usePaginatedQueryGeneric
-   useQueriesGeneric
-   OptimisticLocalStore

## React Hooks​

### useQuery​

-   **`useQuery(name: string, ...args: Value[]): Value | undefined`**

Load a reactive query within a React component.

This React hook contains internal state that will cause a rerender
whenever the query result changes.

This relies on the `ConvexProvider` being above in the React component
tree.

#### Parameters​

  Name        Type        Description
  ----------- ----------- --------------------------------------
  `name`      `string`    The name of the query function.
  `...args`   `Value[]`   The arguments to the query function.

#### Returns​

`Value | undefined`

`undefined` if loading and the query\'s return value otherwise.

------------------------------------------------------------------------

### useMutation​

-   **`useMutation(name: string): ReactMutation`**

Construct a new `ReactMutation`.

Mutation objects can be called like functions to request execution of
the corresponding Convex function, or further configured with optimistic
updates.

The value returned by this hook is stable across renders, so it can be
used by React dependency arrays and memoization logic relying on object
identity without causing rerenders.

This relies on the `ConvexProvider` being above in the React component
tree.

#### Parameters​

  Name     Type       Description
  -------- ---------- ---------------------------
  `name`   `string`   The name of the mutation.

#### Returns​

`ReactMutation`

The `ReactMutation` object with that name.

------------------------------------------------------------------------

### useConvex​

-   **`useConvex()`**

Get the `ConvexReactClient` within a React component.

This relies on the `ConvexProvider` being above in the React component
tree.

#### Returns​

`ConvexReactClient | undefined`

The active ConvexReactClient object, or `undefined`.

### usePaginatedQuery​

-   **usePaginatedQuery**(`name`, `options`, \...`args`):
    `UsePaginatedQueryResult``<any>`

Load data reactively from a paginated query to a create a growing list.

This can be used to power \"infinite scroll\" UIs.

This hook must be used with Convex query functions that match
PaginatedQueryFunction. This means they must:

1.  Have a first argument must be an object containing `numItems` and
    `cursor`.
2.  Return a PaginationResult.

`usePaginatedQuery` concatenates all the pages of results into a single
list and manages the continuation cursors when requesting more items.

Example usage:

<div>

<div>

    const { results, status, loadMore } = usePaginatedQuery(
      "listMessages",
      { initialNumItems: 5 },
      "#general"
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

If the query `name` or `args` change, the pagination state will be reset
to the first page. Similarly, if any of the pages result in an
InvalidCursor or QueryScannedTooManyDocumentsError error, the pagination
state will also reset to the first page.

To learn more about pagination, see Paginated Queries.

#### Parameters​

  Name        Type          Description
  ----------- ------------- ----------------------------------------------------------------------------
  `name`      `string`      The name of the query function.
  `options`   `Object`      An object specifying the `initialNumItems` to be loaded in the first page.
  `...args`   `Value`\[\]   The arguments to the query function, excluding the first.

#### Returns​

`UsePaginatedQueryResult``<any>`

A UsePaginatedQueryResult that includes the currently loaded items, the
status of the pagination, and a `loadMore` function.

### useQueries​

-   **useQueries**(`queries`): `Record<string`, `any` \| `undefined` \|
    `Error>`

Load a variable number of reactive Convex queries.

`useQueries` is similar to useQuery but it allows loading multiple
queries which can be useful for loading a dynamic number of queries
without violating the rules of React hooks.

This hook accepts an object whose keys are identifiers for each query
and the values are objects of `{ name: string, args: Value[] }`. The
`name` is the name of the Convex query function to load, and the `args`
are the arguments to that function.

The hook returns an object that maps each identifier to the result of
the query, `undefined` if the query is still loading, or an instance of
`Error` if the query threw an exception.

For example if you loaded a query like:

<div>

<div>

    const results = useQueries({
      messagesInGeneral: {
        name: "listMessages",
        args: ["#general"],
      },
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

then the result would look like:

<div>

<div>

    {
      messagesInGeneral: [{
        channel: "#general",
        body: "hello"
        _id: ...,
        _creationTime: ...
      }]
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This React hook contains internal state that will cause a rerender
whenever any of the query results change.

Throws an error if not used under ConvexProvider.

#### Parameters​

  Name        Type                  Description
  ----------- --------------------- -------------------------------------------------------------------------------------------------------------------------
  `queries`   `RequestForQueries`   An object mapping identifiers to objects of `{name: string, args: Value[] }` describing which query functions to fetch.

#### Returns​

`Record<string`, `any` \| `undefined` \| `Error>`

An object with the same keys as the input. The values are the result of
the query function, `undefined` if it\'s still loading, or an `Error` if
it threw an exception.

## Types​

### OptimisticLocalStore​

A view of the query results currently in the Convex client for use
within optimistic updates.

This is an alias of `OptimisticLocalStore` that is typed for your app\'s
API.

</div>

</div>

</div>

</div>

</div>
