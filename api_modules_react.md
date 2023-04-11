<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/react

<div>

On this page

</div>

<div>

<div>

# Module: react

</div>

Tools to integrate Convex into React applications.

This module contains:

1.  ConvexReactClient, a client for using Convex in React.
2.  ConvexProvider, a component that stores this client in React
    context.
3.  Authenticated, Unauthenticated and AuthLoading helper auth
    components.
4.  Hooks for calling into this client within your React components.

## Usage​

### Creating the client​

<div>

<div>

    import { ConvexReactClient } from "convex/react";

    // typically loaded from an environment variable
    const address = "https://small-mouse-123.convex.cloud"
    const convex = new ConvexReactClient(address);

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Storing the client in React Context​

<div>

<div>

    import { ConvexProvider } from "convex/react";

    <ConvexProvider client={convex}>
      <App />
    </ConvexProvider>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Using the auth helpers​

<div>

<div>

    import { Authenticated, Unauthenticated, AuthLoading } from "convex/react";

    <Authenticated>
      Logged in
    </Authenticated>
    <Unauthenticated>
      Logged out
    </Unauthenticated>
    <AuthLoading>
      Still loading
    </AuthLoading>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Generating typed hooks​

This module is typically used alongside generated hooks.

To generate the hooks, run `npx convex dev` in your Convex project. This
will create a `convex/_generated/react.js` file with the following React
hooks, typed for your queries and mutations:

-   useQuery
-   useMutation
-   useConvex
-   usePaginatedQuery
-   useQueries

If you aren\'t using code generation, you can use these untyped hooks
instead:

-   useQueryGeneric
-   useMutationGeneric
-   useConvexGeneric
-   usePaginatedQueryGeneric
-   useQueriesGeneric

### Using the hooks​

<div>

<div>

    import { useQuery, useMutation } from "../convex/_generated/react";

    function App() {
      const counter = useQuery("getCounter");
      const increment = useMutation("incrementCounter");
      // Your component here!
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Interfaces​

-   ReactMutation
-   ReactAction
-   Watch
-   ReactClientOptions

## Classes​

-   ConvexReactClient

## Type Aliases​

### AuthTokenFetcher​

Ƭ **AuthTokenFetcher**: () =\> `Promise`\<`string` \| `null` \|
`undefined`\>

#### Type declaration​

▸ (): `Promise`\<`string` \| `null` \| `undefined`\>

An async function returning the JWT-encoded OpenID Connect Identity
Token if available. See setAuth.

##### Returns​

`Promise`\<`string` \| `null` \| `undefined`\>

------------------------------------------------------------------------

### ConvexAuthState​

Ƭ **ConvexAuthState**: `Object`

Type representing the state of an auth integration with Convex.

#### Type declaration​

  Name                Type
  ------------------- -----------
  `isLoading`         `boolean`
  `isAuthenticated`   `boolean`

------------------------------------------------------------------------

### UseQueryForAPI​

Ƭ **UseQueryForAPI**\<`API`\>: \<Name\>(`name`: `Name`, \...`args`:
`Parameters`\<`NamedQuery`\<`API`, `Name`\>\>) =\>
`ReturnType`\<`NamedQuery`\<`API`, `Name`\>\> \| `undefined`

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ \<`Name`\>(`name`, `...args`): `ReturnType`\<`NamedQuery`\<`API`,
`Name`\>\> \| `undefined`

Internal type helper used by Convex code generation.

Used to give useQueryGeneric a type specific to your API.

##### Type parameters​

  Name     Type
  -------- -------------------------------------
  `Name`   extends `PublicQueryNames`\<`API`\>

##### Parameters​

  Name        Type
  ----------- -----------------------------------------------
  `name`      `Name`
  `...args`   `Parameters`\<`NamedQuery`\<`API`, `Name`\>\>

##### Returns​

`ReturnType`\<`NamedQuery`\<`API`, `Name`\>\> \| `undefined`

------------------------------------------------------------------------

### UseMutationForAPI​

Ƭ **UseMutationForAPI**\<`API`\>: \<Name\>(`name`: `Name`) =\>
`ReactMutation`\<`API`, `Name`\>

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ \<`Name`\>(`name`): `ReactMutation`\<`API`, `Name`\>

Internal type helper used by Convex code generation.

Used to give useMutationGeneric a type specific to your API.

##### Type parameters​

  Name     Type
  -------- ----------------------------------------
  `Name`   extends `PublicMutationNames`\<`API`\>

##### Parameters​

  Name     Type
  -------- --------
  `name`   `Name`

##### Returns​

`ReactMutation`\<`API`, `Name`\>

------------------------------------------------------------------------

### UseActionForAPI​

Ƭ **UseActionForAPI**\<`API`\>: \<Name\>(`name`: `Name`) =\>
`ReactAction`\<`API`, `Name`\>

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ \<`Name`\>(`name`): `ReactAction`\<`API`, `Name`\>

Internal type helper used by Convex code generation.

Used to give useMutationGeneric a type specific to your API.

##### Type parameters​

  Name     Type
  -------- --------------------------------------
  `Name`   extends `PublicActionNames`\<`API`\>

##### Parameters​

  Name     Type
  -------- --------
  `name`   `Name`

##### Returns​

`ReactAction`\<`API`, `Name`\>

------------------------------------------------------------------------

### UseConvexForAPI​

Ƭ **UseConvexForAPI**\<`API`\>: () =\> `ConvexReactClient`\<`API`\>

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ (): `ConvexReactClient`\<`API`\>

Internal type helper used by Convex code generation.

Used to give useConvexGeneric a type specific to your API.

##### Returns​

`ConvexReactClient`\<`API`\>

------------------------------------------------------------------------

### UsePaginatedQueryResult​

Ƭ **UsePaginatedQueryResult**\<`T`\>: { `results`: `T`\[\] } & {
`status`: `"CanLoadMore"` ; `loadMore`: (`numItems`: `number`) =\>
`void` } \| { `status`: `"LoadingMore"` ; `loadMore`: `undefined` } \| {
`status`: `"Exhausted"` ; `loadMore`: `undefined` }

The result of calling the usePaginatedQueryGeneric hook.

This includes:

1.  `results` - An array of the currently loaded results.
2.  `status` - The status of the pagination. The possible statuses are:

-   \"CanLoadMore\": This query may have more items to fetch. Call
    `loadMore` to fetch another page.
-   \"LoadingMore\": We\'re currently loading another page of results.
-   \"Exhausted\": We\'ve paginated to the end of the list.

1.  `loadMore` A callback to fetch more results. This will be
    `undefined` unless the status is \"CanLoadMore\".

#### Type parameters​

  Name
  ------
  `T`

------------------------------------------------------------------------

### PaginatedQueryFunction​

Ƭ **PaginatedQueryFunction**\<`Args`, `ReturnType`\>:
(`paginationOptions`: `PaginationOptions`, \...`args`: `Args`) =\>
`PaginationResult`\<`ReturnType`\>

#### Type parameters​

  Name           Type
  -------------- -------------------
  `Args`         extends `any`\[\]
  `ReturnType`   `ReturnType`

#### Type declaration​

▸ (`paginationOptions`, `...args`): `PaginationResult`\<`ReturnType`\>

A query function that is usable with usePaginatedQueryGeneric.

The function\'s first argument must be a PaginationOptions object. The
function must return a PaginationResult.

##### Parameters​

  Name                  Type
  --------------------- ---------------------
  `paginationOptions`   `PaginationOptions`
  `...args`             `Args`

##### Returns​

`PaginationResult`\<`ReturnType`\>

------------------------------------------------------------------------

### PaginatedQueryNames​

Ƭ **PaginatedQueryNames**\<`API`\>: keyof
`PickByValue`\<`API`\[`"publicQueries"`\],
`PaginatedQueryFunction`\<`any`, `any`\>\> & `string`

The names of the paginated query functions in a Convex API.

These are normal query functions that match PaginatedQueryFunction.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

------------------------------------------------------------------------

### PaginatedQueryArgs​

Ƭ **PaginatedQueryArgs**\<`Query`\>: `Query` extends
`PaginatedQueryFunction`\<infer Args, `any`\> ? `Args` : `never`

The type of the arguments to a PaginatedQueryFunction.

This type includes all the arguments after the initial PaginationOptions
argument.

#### Type parameters​

  Name      Type
  --------- --------------------------------------------------
  `Query`   extends `PaginatedQueryFunction`\<`any`, `any`\>

------------------------------------------------------------------------

### PaginatedQueryReturnType​

Ƭ **PaginatedQueryReturnType**\<`Query`\>: `Query` extends
`PaginatedQueryFunction`\<`any`, infer ReturnType\> ? `ReturnType` :
`never`

The return type of a PaginatedQueryFunction.

This is the type of the inner document or object within the
PaginationResult that a paginated query function returns.

#### Type parameters​

  Name      Type
  --------- --------------------------------------------------
  `Query`   extends `PaginatedQueryFunction`\<`any`, `any`\>

------------------------------------------------------------------------

### UsePaginatedQueryForAPI​

Ƭ **UsePaginatedQueryForAPI**\<`API`\>: \<Name\>(`name`: `Name`,
`options`: { `initialNumItems`: `number` }, \...`args`:
`PaginatedQueryArgs`\<`NamedQuery`\<`API`, `Name`\>\>) =\>
`UsePaginatedQueryResult`\<`PaginatedQueryReturnType`\<`NamedQuery`\<`API`,
`Name`\>\>\>

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ \<`Name`\>(`name`, `options`, `...args`):
`UsePaginatedQueryResult`\<`PaginatedQueryReturnType`\<`NamedQuery`\<`API`,
`Name`\>\>\>

Internal type helper used by Convex code generation.

Used to give usePaginatedQueryGeneric a type specific to your API.

##### Type parameters​

  Name     Type
  -------- ----------------------------------------
  `Name`   extends `PaginatedQueryNames`\<`API`\>

##### Parameters​

  Name                        Type
  --------------------------- -------------------------------------------------------
  `name`                      `Name`
  `options`                   `Object`
  `options.initialNumItems`   `number`
  `...args`                   `PaginatedQueryArgs`\<`NamedQuery`\<`API`, `Name`\>\>

##### Returns​

`UsePaginatedQueryResult`\<`PaginatedQueryReturnType`\<`NamedQuery`\<`API`,
`Name`\>\>\>

------------------------------------------------------------------------

### RequestForQueries​

Ƭ **RequestForQueries**: `Record`\<`string`, { `name`: `string` ;
`args`: `Value`\[\] }\>

An object representing a request to load multiple queries.

The keys of this object are identifiers and the values are objects
containing the name of the query function and the arguments to pass to
it.

This is used as an argument to useQueriesGeneric.

------------------------------------------------------------------------

### UseQueriesForAPI​

Ƭ **UseQueriesForAPI**\<`API`\>: \<QueryNameMap\>(`queries`: {
\[Identifier in keyof QueryNameMap\]: Object }) =\> { \[Identifier in
keyof QueryNameMap\]: ReturnType\<NamedQuery\<API,
QueryNameMap\[Identifier\]\>\> \| undefined \| Error }

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ \<`QueryNameMap`\>(`queries`): { \[Identifier in keyof QueryNameMap\]:
ReturnType\<NamedQuery\<API, QueryNameMap\[Identifier\]\>\> \| undefined
\| Error }

Internal type helper used by Convex code generation.

Used to give useQueriesGeneric a type specific to your API.

##### Type parameters​

  Name             Type
  ---------------- -----------------------------------------------------------
  `QueryNameMap`   extends `Record`\<`string`, `PublicQueryNames`\<`API`\>\>

##### Parameters​

  Name        Type
  ----------- --------------------------------------------------
  `queries`   { \[Identifier in keyof QueryNameMap\]: Object }

##### Returns​

{ \[Identifier in keyof QueryNameMap\]: ReturnType\<NamedQuery\<API,
QueryNameMap\[Identifier\]\>\> \| undefined \| Error }

## Functions​

### useConvexAuth​

▸ **useConvexAuth**(): `Object`

Get the ConvexAuthState within a React component.

This relies on a Convex auth integration provider being above in the
React component tree.

#### Returns​

`Object`

The current ConvexAuthState.

  Name                Type
  ------------------- -----------
  `isLoading`         `boolean`
  `isAuthenticated`   `boolean`

------------------------------------------------------------------------

### ConvexProviderWithAuth​

▸ **ConvexProviderWithAuth**(`«destructured»`): `Element`

A replacement for ConvexProvider which additionally provides
ConvexAuthState to descendants of this component.

Use this to integrate any auth provider with Convex. The `useAuth` prop
should be a React hook that returns the provider\'s authentication state
and a function to fetch a JWT access token.

See Custom Auth Integration for more information.

#### Parameters​

  Name               Type
  ------------------ -------------------------------------------------------------------------------------------------------------------------------
  `«destructured»`   `Object`
  › `children?`      `ReactNode`
  › `client`         `IConvexReactClient`
  › `useAuth`        () =\> { `isLoading`: `boolean` ; `isAuthenticated`: `boolean` ; `fetchAccessToken`: () =\> `Promise`\<`null` \| `string`\> }

#### Returns​

`Element`

------------------------------------------------------------------------

### Authenticated​

▸ **Authenticated**(`«destructured»`): `ReactNode`

Renders children if the client is authenticated.

#### Parameters​

  Name               Type
  ------------------ -------------
  `«destructured»`   `Object`
  › `children`       `ReactNode`

#### Returns​

`ReactNode`

------------------------------------------------------------------------

### Unauthenticated​

▸ **Unauthenticated**(`«destructured»`): `ReactNode`

Renders children if the client is using authentication but is not
authenticated.

#### Parameters​

  Name               Type
  ------------------ -------------
  `«destructured»`   `Object`
  › `children`       `ReactNode`

#### Returns​

`ReactNode`

------------------------------------------------------------------------

### AuthLoading​

▸ **AuthLoading**(`«destructured»`): `ReactNode`

Renders children if the client isn\'t using authentication or is in the
process of authenticating.

#### Parameters​

  Name               Type
  ------------------ -------------
  `«destructured»`   `Object`
  › `children`       `ReactNode`

#### Returns​

`ReactNode`

------------------------------------------------------------------------

### useConvexGeneric​

▸ **useConvexGeneric**\<`API`\>(): `ConvexReactClient`\<`API`\>

Get the ConvexReactClient within a React component.

This relies on the ConvexProvider being above in the React component
tree.

If you\'re using code generation, use the `useConvex` function in
`convex/_generated/react.js` which is typed for your API.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Returns​

`ConvexReactClient`\<`API`\>

The active ConvexReactClient object, or `undefined`.

------------------------------------------------------------------------

### ConvexProvider​

▸ **ConvexProvider**(`props`, `context?`): `null` \|
`ReactElement`\<`any`, `any`\>

Provides an active Convex ConvexReactClient to descendants of this
component.

Wrap your app in this component to use Convex hooks `useQuery`,
`useMutation`, and `useConvex`.

#### Parameters​

  Name         Type                                                                                           Description
  ------------ ---------------------------------------------------------------------------------------------- ------------------------------------------------------------------------
  `props`      `PropsWithChildren`\<{ `client`: `ConvexReactClient`\<`any`\> ; `children?`: `ReactNode` }\>   an object with a `client` property that refers to a ConvexReactClient.
  `context?`   `any`                                                                                          \-

#### Returns​

`null` \| `ReactElement`\<`any`, `any`\>

------------------------------------------------------------------------

### useQueryGeneric​

▸ **useQueryGeneric**\<`API`, `Name`\>(`name`, `...args`):
`ReturnType`\<`NamedQuery`\<`API`, `Name`\>\> \| `undefined`

Load a reactive query within a React component.

This React hook contains internal state that will cause a rerender
whenever the query result changes.

Throws an error if not used under ConvexProvider.

If you\'re using code generation, use the `useQuery` function in
`convex/_generated/react.js` which is typed for your API.

#### Type parameters​

  Name     Type
  -------- ----------------------
  `API`    extends `GenericAPI`
  `Name`   extends `string`

#### Parameters​

  Name        Type                                            Description
  ----------- ----------------------------------------------- --------------------------------------
  `name`      `Name`                                          The name of the query function.
  `...args`   `Parameters`\<`NamedQuery`\<`API`, `Name`\>\>   The arguments to the query function.

#### Returns​

`ReturnType`\<`NamedQuery`\<`API`, `Name`\>\> \| `undefined`

`undefined` if loading and the query\'s return value otherwise.

------------------------------------------------------------------------

### useMutationGeneric​

▸ **useMutationGeneric**\<`API`, `Name`\>(`name`):
`ReactMutation`\<`API`, `Name`\>

Construct a new ReactMutation.

Mutation objects can be called like functions to request execution of
the corresponding Convex function, or further configured with optimistic
updates.

The value returned by this hook is stable across renders, so it can be
used by React dependency arrays and memoization logic relying on object
identity without causing rerenders.

If you\'re using code generation, use the `useMutation` function in
`convex/_generated/react.js` which is typed for your API.

Throws an error if not used under ConvexProvider.

#### Type parameters​

  Name     Type
  -------- ----------------------
  `API`    extends `GenericAPI`
  `Name`   extends `string`

#### Parameters​

  Name     Type     Description
  -------- -------- ---------------------------
  `name`   `Name`   The name of the mutation.

#### Returns​

`ReactMutation`\<`API`, `Name`\>

The ReactMutation object with that name.

------------------------------------------------------------------------

### useActionGeneric​

▸ **useActionGeneric**\<`API`, `Name`\>(`name`): `ReactAction`\<`API`,
`Name`\>

Construct a new ReactAction.

Action objects can be called like functions to request execution of the
corresponding Convex function.

The value returned by this hook is stable across renders, so it can be
used by React dependency arrays and memoization logic relying on object
identity without causing rerenders.

If you\'re using code generation, use the `useAction` function in
`convex/_generated/react.js` which is typed for your API.

Throws an error if not used under ConvexProvider.

#### Type parameters​

  Name     Type
  -------- ----------------------
  `API`    extends `GenericAPI`
  `Name`   extends `string`

#### Parameters​

  Name     Type     Description
  -------- -------- -------------------------
  `name`   `Name`   The name of the action.

#### Returns​

`ReactAction`\<`API`, `Name`\>

The ReactAction object with that name.

------------------------------------------------------------------------

### usePaginatedQueryGeneric​

▸ **usePaginatedQueryGeneric**(`name`, `options`, `...args`):
`UsePaginatedQueryResult`\<`any`\>

Load data reactively from a paginated query to a create a growing list.

This can be used to power \"infinite scroll\" UIs.

This hook must be used with Convex query functions that match
PaginatedQueryFunction. This means they must:

1.  Have a first argument must be an object containing `numItems` and
    `cursor`.
2.  Return a PaginationResult.

`usePaginatedQueryGeneric` concatenates all the pages of results into a
single list and manages the continuation cursors when requesting more
items.

Example usage:

<div>

<div>

    const { results, status, loadMore } = usePaginatedQueryGeneric(
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
InvalidCursor or QueryScannedTooManyDocuments error, the pagination
state will also reset to the first page.

To learn more about pagination, see Paginated Queries.

If you\'re using code generation, use the `usePaginatedQuery` function
in `convex/_generated/react.js` which is typed for your API.

#### Parameters​

  Name                        Type          Description
  --------------------------- ------------- ----------------------------------------------------------------------------
  `name`                      `string`      The name of the query function.
  `options`                   `Object`      An object specifying the `initialNumItems` to be loaded in the first page.
  `options.initialNumItems`   `number`      \-
  `...args`                   `Value`\[\]   The arguments to the query function, excluding the first.

#### Returns​

`UsePaginatedQueryResult`\<`any`\>

A UsePaginatedQueryResult that includes the currently loaded items, the
status of the pagination, and a `loadMore` function.

------------------------------------------------------------------------

### optimisticallyUpdateValueInPaginatedQuery​

▸ **optimisticallyUpdateValueInPaginatedQuery**\<`API`,
`Name`\>(`localStore`, `name`, `args`, `updateValue`): `void`

Optimistically update the values in a paginated list.

This optimistic update is designed to be used to update data loaded with
usePaginatedQueryGeneric. It updates the list by applying `updateValue`
to each element of the list across all of the loaded pages.

This will only apply to queries with a matching names and arguments.

Example usage:

<div>

<div>

    const myMutation = useMutation("myMutationName")
    .withOptimisticUpdate((localStore, mutationArg) => {

      // Optimistically update the document with ID `mutationArg`
      // to have an additional property.

      optimisticallyUpdateValueInPaginatedQuery(
        localStore,
        "paginatedQueryName",
        [],
        currentValue => {
          if (mutationArg.equals(currentValue._id)) {
            return {
              ...currentValue,
              "newProperty": "newValue",
            };
          }
          return currentValue;
        }
      );

    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Type parameters​

  Name     Type
  -------- ----------------------
  `API`    extends `GenericAPI`
  `Name`   extends `string`

#### Parameters​

  Name            Type                                                                                                                                            Description
  --------------- ----------------------------------------------------------------------------------------------------------------------------------------------- -----------------------------------------------------------
  `localStore`    `OptimisticLocalStore`\<`API`\>                                                                                                                 \-
  `name`          `Name`                                                                                                                                          The name of the paginated query function.
  `args`          `PaginatedQueryArgs`\<`NamedQuery`\<`API`, `Name`\>\>                                                                                           The arguments to the query function, excluding the first.
  `updateValue`   (`currentValue`: `PaginatedQueryReturnType`\<`NamedQuery`\<`API`, `Name`\>\>) =\> `PaginatedQueryReturnType`\<`NamedQuery`\<`API`, `Name`\>\>   A function to produce the new values.

#### Returns​

`void`

------------------------------------------------------------------------

### useQueriesGeneric​

▸ **useQueriesGeneric**(`queries`): `Record`\<`string`, `any` \|
`undefined` \| `Error`\>

Load a variable number of reactive Convex queries.

`useQueriesGeneric` is similar to useQueryGeneric but it allows loading
multiple queries which can be useful for loading a dynamic number of
queries without violating the rules of React hooks.

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

    const results = useQueriesGeneric({
      messagesInGeneral: {
        name: "listMessages",
        args: ["#general"]
      }
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

If you\'re using code generation, use the `useQueries` function in
`convex/_generated/react.js` which is typed for your API.

#### Parameters​

  Name        Type                  Description
  ----------- --------------------- -------------------------------------------------------------------------------------------------------------------------
  `queries`   `RequestForQueries`   An object mapping identifiers to objects of `{name: string, args: Value[] }` describing which query functions to fetch.

#### Returns​

`Record`\<`string`, `any` \| `undefined` \| `Error`\>

An object with the same keys as the input. The values are the result of
the query function, `undefined` if it\'s still loading, or an `Error` if
it threw an exception.

</div>

</div>

</div>

</div>

</div>
