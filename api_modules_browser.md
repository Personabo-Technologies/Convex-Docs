<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/browser

<div>

On this page

</div>

<div>

<div>

# Module: browser

</div>

Tools for accessing Convex in the browser.

**If you are using React, use the react module instead.**

## Usage​

Create a ConvexHttpClient to connect to the Convex Cloud.

<div>

<div>

    import { ConvexHttpClient } from "convex/browser";
    // typically loaded from an environment variable
    const address = "https://small-mouse-123.convex.cloud";
    const convex = new ConvexHttpClient(address);

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Interfaces​

-   Query
-   Mutation
-   ClientOptions
-   OptimisticLocalStore

## Classes​

-   ConvexHttpClient
-   InternalConvexClient

## Type Aliases​

### GenericAPI​

Ƭ **GenericAPI**: `Object`

Description of the Convex functions available to an application.

This is a generic type that expresses the shape of API types created by
`npx convex codegen`. It\'s used to make the Convex clients type-safe.

#### Type declaration​

  Name                Type
  ------------------- ---------------------------------------------------------
  `publicQueries`     `Record`\<`string`, (\...`args`: `any`\[\]) =\> `any`\>
  `allQueries`        `Record`\<`string`, (\...`args`: `any`\[\]) =\> `any`\>
  `publicMutations`   `Record`\<`string`, (\...`args`: `any`\[\]) =\> `any`\>
  `allMutations`      `Record`\<`string`, (\...`args`: `any`\[\]) =\> `any`\>
  `publicActions`     `Record`\<`string`, (\...`args`: `any`\[\]) =\> `any`\>
  `allActions`        `Record`\<`string`, (\...`args`: `any`\[\]) =\> `any`\>

------------------------------------------------------------------------

### QueryNames​

Ƭ **QueryNames**\<`API`\>: keyof `API`\[`"allQueries"`\] & `string`

The names of query functions in a Convex API.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

------------------------------------------------------------------------

### PublicQueryNames​

Ƭ **PublicQueryNames**\<`API`\>: keyof `API`\[`"publicQueries"`\] &
`string`

The names of public query functions in a Convex API.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

------------------------------------------------------------------------

### MutationNames​

Ƭ **MutationNames**\<`API`\>: keyof `API`\[`"allMutations"`\] & `string`

The names of mutation functions in a Convex API.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

------------------------------------------------------------------------

### PublicMutationNames​

Ƭ **PublicMutationNames**\<`API`\>: keyof `API`\[`"publicMutations"`\] &
`string`

The names of public mutation functions in a Convex API.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

------------------------------------------------------------------------

### ActionNames​

Ƭ **ActionNames**\<`API`\>: keyof `API`\[`"allActions"`\] & `string`

The names of actions in a Convex API.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

------------------------------------------------------------------------

### PublicActionNames​

Ƭ **PublicActionNames**\<`API`\>: keyof `API`\[`"publicActions"`\] &
`string`

The names of public query functions in a Convex API.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

------------------------------------------------------------------------

### NamedQuery​

Ƭ **NamedQuery**\<`API`, `Name`\>: `API`\[`"allQueries"`\]\[`Name`\]

The type of a query function in a Convex API.

#### Type parameters​

  Name     Type
  -------- -------------------------------
  `API`    extends `GenericAPI`
  `Name`   extends `QueryNames`\<`API`\>

------------------------------------------------------------------------

### NamedMutation​

Ƭ **NamedMutation**\<`API`, `Name`\>:
`API`\[`"allMutations"`\]\[`Name`\]

The type of a mutation function in a Convex API.

#### Type parameters​

  Name     Type
  -------- ----------------------------------
  `API`    extends `GenericAPI`
  `Name`   extends `MutationNames`\<`API`\>

------------------------------------------------------------------------

### NamedAction​

Ƭ **NamedAction**\<`API`, `Name`\>: `API`\[`"allActions"`\]\[`Name`\]

The type of an action in a Convex API.

#### Type parameters​

  Name     Type
  -------- --------------------------------
  `API`    extends `GenericAPI`
  `Name`   extends `ActionNames`\<`API`\>

------------------------------------------------------------------------

### ApiFromModules​

Ƭ **ApiFromModules**\<`Modules`\>: `Object`

Create the API type from the types of all of the modules.

Input is an object mapping file paths to the type of each module.

For internal use by Convex code generation.

#### Type parameters​

  Name        Type
  ----------- -----------------------------------------------------------
  `Modules`   extends `Record`\<`string`, `Record`\<`string`, `any`\>\>

#### Type declaration​

  Name                Type
  ------------------- ------------------------------------------------------------------------------------------------------------------------------------------
  `publicQueries`     `Expand`\<`ConvertToClientFunctions`\<`PickByValue`\<`MergeAllExports`\<`Modules`\>, { `isQuery`: `true` ; `isPublic`: `true` }\>\>\>
  `allQueries`        `Expand`\<`ConvertToClientFunctions`\<`PickByValue`\<`MergeAllExports`\<`Modules`\>, { `isQuery`: `true` }\>\>\>
  `publicMutations`   `Expand`\<`ConvertToClientFunctions`\<`PickByValue`\<`MergeAllExports`\<`Modules`\>, { `isMutation`: `true` ; `isPublic`: `true` }\>\>\>
  `allMutations`      `Expand`\<`ConvertToClientFunctions`\<`PickByValue`\<`MergeAllExports`\<`Modules`\>, { `isMutation`: `true` }\>\>\>
  `publicActions`     `Expand`\<`ConvertToClientFunctions`\<`PickByValue`\<`MergeAllExports`\<`Modules`\>, { `isAction`: `true` ; `isPublic`: `true` }\>\>\>
  `allActions`        `Expand`\<`ConvertToClientFunctions`\<`PickByValue`\<`MergeAllExports`\<`Modules`\>, { `isAction`: `true` }\>\>\>

------------------------------------------------------------------------

### OptimisticUpdate​

Ƭ **OptimisticUpdate**\<`API`, `Arguments`\>: (`localQueryStore`:
`OptimisticLocalStore`\<`API`\>, \...`args`: `Arguments`) =\> `void`

#### Type parameters​

  Name          Type
  ------------- ----------------------
  `API`         extends `GenericAPI`
  `Arguments`   extends `Value`\[\]

#### Type declaration​

▸ (`localQueryStore`, `...args`): `void`

A temporary, local update to query results within this client.

This update will always be executed when a mutation is synced to the
Convex server and rolled back when the mutation completes.

Note that optimistic updates can be called multiple times! If the client
loads new data while the mutation is in progress, the update will be
replayed again.

##### Parameters​

  Name                Type                              Description
  ------------------- --------------------------------- ----------------------------------------------------
  `localQueryStore`   `OptimisticLocalStore`\<`API`\>   An interface to read and edit local query results.
  `...args`           `Arguments`                       The arguments to the mutation.

##### Returns​

`void`

------------------------------------------------------------------------

### QueryJournal​

Ƭ **QueryJournal**: `string` \| `null`

A serialized representation of decisions made during a query\'s
execution.

A journal is produced when a query function first executes and is
re-used when a query is re-executed.

Currently this is used to store pagination end cursors to ensure that
pages of paginated queries will always end at the same cursor. This
enables gapless, reactive pagination.

`null` is used to represent empty journals.

------------------------------------------------------------------------

### QueryResult​

Ƭ **QueryResult**: { `success`: `true` ; `value`: `Value` } \| {
`success`: `false` ; `errorMessage`: `string` }

The result of running a query function on the server.

If the function hit an exception it will have an `errorMessage`.
Otherwise it will produce a `Value`.

------------------------------------------------------------------------

### QueryToken​

Ƭ **QueryToken**: `string`

A string representing the name and arguments of a query.

This is used by the InternalConvexClient.

</div>

</div>

</div>

</div>

</div>
