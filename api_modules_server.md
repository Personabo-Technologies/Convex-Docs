<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server

<div>

On this page

</div>

<div>

<div>

# Module: server

</div>

Utilities for implementing server-side Convex query and mutation
functions.

## Usage​

### Code Generation​

This module is typically used alongside generated server code.

To generate the server code, run `npx convex codegen` in your Convex
project. This will create a `convex/_generated/server.js` file with the
following functions, typed for your schema:

-   query
-   mutation

If you aren\'t using TypeScript and code generation, you can use these
untyped functions instead:

-   queryGeneric
-   mutationGeneric

### Example​

Convex functions are defined by using either the `query` or `mutation`
wrappers.

Queries receive a `db` that implements the DatabaseReader interface.

<div>

<div>

    import { query } from "./_generated/server";

    export default query(async ({ db }, { arg1, arg2 }) => {
      // Your (read-only) code here!
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

If your function needs to write to the database, such as inserting,
updating, or deleting documents, use `mutation` instead which provides a
`db` that implements the DatabaseWriter interface.

<div>

<div>

    import { mutation } from "./_generated/server";

    export default mutation(async ({ db }, { arg1, arg2 }) => {
      // Your mutation code here!
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Interfaces​

-   UserIdentity
-   Auth
-   CronJob
-   DatabaseReader
-   DatabaseWriter
-   FilterBuilder
-   IndexRangeBuilder
-   PaginationResult
-   PaginationOptions
-   QueryInitializer
-   Query
-   OrderedQuery
-   ActionCtx
-   HttpEndpointCtx
-   Scheduler
-   SearchFilterBuilder
-   SearchFilterFinalizer
-   StorageReader
-   StorageWriter
-   StorageHttpWriter

## Classes​

-   Expression
-   IndexRange
-   HttpRouter
-   SearchFilter

## Functions​

### cronJobsGeneric​

▸ **cronJobsGeneric**\<`API`\>(): `Crons`\<`API`\>

Internal type helper used by Convex code generation.

If you\'re using code generation, use the `cronJobs` function in
`convex/_generated/server.js` which is typed for your API.

<div>

<div>

    // convex/crons.js
    import { cronJobs } from 'convex/server';

    const crons = cronJobs();
    crons.weekly(
      "weekly re-engagement email",
      {
        hourUTC: 17, // (9:30am Pacific/10:30am Daylight Savings Pacific)
        minuteUTC: 30,
      },
      "sendEmails"
    )
    export default crons;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Returns​

`Crons`\<`API`\>

------------------------------------------------------------------------

### mutationGeneric​

▸ **mutationGeneric**\<`DataModel`, `API`, `Args`, `Output`\>(`func`):
`PublicMutation`\<`Args`, `Output`\>

Define a mutation in this Convex app\'s public API.

This function will be allowed to modify your Convex database and will be
accessible from the client.

If you\'re using code generation, use the `mutation` function in
`convex/_generated/server.d.ts` which is typed for your data model.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`
  `API`         extends `GenericAPI`
  `Args`        extends `any`\[\]
  `Output`      `Output`

#### Parameters​

  Name     Type                                                                            Description
  -------- ------------------------------------------------------------------------------- -------------------------------------------------------------------------
  `func`   (`ctx`: `MutationCtx`\<`DataModel`, `API`\>, \...`args`: `Args`) =\> `Output`   The mutation function. It receives a MutationCtx as its first argument.

#### Returns​

`PublicMutation`\<`Args`, `Output`\>

The wrapped mutation. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### internalMutationGeneric​

▸ **internalMutationGeneric**\<`DataModel`, `API`, `Args`,
`Output`\>(`func`): `InternalMutation`\<`Args`, `Output`\>

Define a mutation that is only accessible from other Convex functions
(but not from the client).

This function will be allowed to modify your Convex database. It will
not be accessible from the client.

If you\'re using code generation, use the `internalMutation` function in
`convex/_generated/server.d.ts` which is typed for your data model.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`
  `API`         extends `GenericAPI`
  `Args`        extends `any`\[\]
  `Output`      `Output`

#### Parameters​

  Name     Type                                                                            Description
  -------- ------------------------------------------------------------------------------- -------------------------------------------------------------------------
  `func`   (`ctx`: `MutationCtx`\<`DataModel`, `API`\>, \...`args`: `Args`) =\> `Output`   The mutation function. It receives a MutationCtx as its first argument.

#### Returns​

`InternalMutation`\<`Args`, `Output`\>

The wrapped mutation. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### queryGeneric​

▸ **queryGeneric**\<`DataModel`, `Args`, `Output`\>(`func`):
`PublicQuery`\<`Args`, `Output`\>

Define a query in this Convex app\'s public API.

This function will be allowed to read your Convex database and will be
accessible from the client.

If you\'re using code generation, use the `query` function in
`convex/_generated/server.d.ts` which is typed for your data model.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`
  `Args`        extends `any`\[\]
  `Output`      `Output`

#### Parameters​

  Name     Type                                                                  Description
  -------- --------------------------------------------------------------------- -------------------------------------------------------------------
  `func`   (`ctx`: `QueryCtx`\<`DataModel`\>, \...`args`: `Args`) =\> `Output`   The query function. It receives a QueryCtx as its first argument.

#### Returns​

`PublicQuery`\<`Args`, `Output`\>

The wrapped query. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### internalQueryGeneric​

▸ **internalQueryGeneric**\<`DataModel`, `Args`, `Output`\>(`func`):
`InternalQuery`\<`Args`, `Output`\>

Define a query that is only accessible from other Convex functions (but
not from the client).

This function will be allowed to read from your Convex database. It will
not be accessible from the client.

If you\'re using code generation, use the `internalQuery` function in
`convex/_generated/server.d.ts` which is typed for your data model.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`
  `Args`        extends `any`\[\]
  `Output`      `Output`

#### Parameters​

  Name     Type                                                                  Description
  -------- --------------------------------------------------------------------- -------------------------------------------------------------------
  `func`   (`ctx`: `QueryCtx`\<`DataModel`\>, \...`args`: `Args`) =\> `Output`   The query function. It receives a QueryCtx as its first argument.

#### Returns​

`InternalQuery`\<`Args`, `Output`\>

The wrapped query. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### actionGeneric​

▸ **actionGeneric**\<`API`, `Args`, `Output`\>(`func`):
`PublicAction`\<`Args`, `Output`\>

Define an action in this Convex app\'s public API.

If you\'re using code generation, use the `action` function in
`convex/_generated/server.d.ts` which is typed for your data model.

#### Type parameters​

  Name       Type
  ---------- ----------------------
  `API`      extends `GenericAPI`
  `Args`     extends `any`\[\]
  `Output`   `Output`

#### Parameters​

  Name     Type                                                             Description
  -------- ---------------------------------------------------------------- --------------------------------------------------------------
  `func`   (`ctx`: `ActionCtx`\<`API`\>, \...`args`: `Args`) =\> `Output`   The function. It receives a ActionCtx as its first argument.

#### Returns​

`PublicAction`\<`Args`, `Output`\>

The wrapped function. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### internalActionGeneric​

▸ **internalActionGeneric**\<`API`, `Args`, `Output`\>(`func`):
`InternalAction`\<`Args`, `Output`\>

Define an action that is only accessible from other Convex functions
(but not from the client).

If you\'re using code generation, use the `internalAction` function in
`convex/_generated/server.d.ts` which is typed for your data model.

#### Type parameters​

  Name       Type
  ---------- ----------------------
  `API`      extends `GenericAPI`
  `Args`     extends `any`\[\]
  `Output`   `Output`

#### Parameters​

  Name     Type                                                             Description
  -------- ---------------------------------------------------------------- --------------------------------------------------------------
  `func`   (`ctx`: `ActionCtx`\<`API`\>, \...`args`: `Args`) =\> `Output`   The function. It receives a ActionCtx as its first argument.

#### Returns​

`InternalAction`\<`Args`, `Output`\>

The wrapped function. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### httpEndpointGeneric​

▸ **httpEndpointGeneric**\<`API`\>(`func`): `PublicHttpEndpoint`

Define a Convex HTTP endpoint.

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Parameters​

  Name     Type                                                                                    Description
  -------- --------------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------
  `func`   (`ctx`: `HttpEndpointCtx`\<`API`\>, `request`: `Request`) =\> `Promise`\<`Response`\>   The function. It receives an HttpEndpointCtx as its first argument, and a `Request` object as its second.

#### Returns​

`PublicHttpEndpoint`

The wrapped endpoint function. Route a URL path to this function in
`convex/http.js`.

------------------------------------------------------------------------

### httpRouter​

▸ **httpRouter**(): `HttpRouter`

Return a new HttpRouter object.

#### Returns​

`HttpRouter`

## Type Aliases​

### CronJobsForAPI​

Ƭ **CronJobsForAPI**\<`API`\>: () =\> { `interval`:
\<Name\>(`identifier`: `string`, `schedule`: `Interval`, `functionName`:
`Name`, \...`args`: `Parameters`\<`NamedSchedulableFunction`\<`API`,
`Name`\>\>) =\> `void` ; `hourly`: \<Name\>(`identifier`: `string`,
`schedule`: `Hourly`, `functionName`: `Name`, \...`args`:
`Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
; `daily`: \<Name\>(`identifier`: `string`, `schedule`: `Daily`,
`functionName`: `Name`, \...`args`:
`Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
; `weekly`: \<Name\>(`identifier`: `string`, `schedule`: `Weekly`,
`functionName`: `Name`, \...`args`:
`Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
; `monthly`: \<Name\>(`identifier`: `string`, `schedule`: `Monthly`,
`functionName`: `Name`, \...`args`:
`Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
; `cron`: \<Name\>(`identifier`: `string`, `cron`: `CronString`,
`functionName`: `Name`, \...`args`:
`Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
}

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ (): `Object`

##### Returns​

`Object`

  Name         Type
  ------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `interval`   \<Name\>(`identifier`: `string`, `schedule`: `Interval`, `functionName`: `Name`, \...`args`: `Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
  `hourly`     \<Name\>(`identifier`: `string`, `schedule`: `Hourly`, `functionName`: `Name`, \...`args`: `Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
  `daily`      \<Name\>(`identifier`: `string`, `schedule`: `Daily`, `functionName`: `Name`, \...`args`: `Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
  `weekly`     \<Name\>(`identifier`: `string`, `schedule`: `Weekly`, `functionName`: `Name`, \...`args`: `Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
  `monthly`    \<Name\>(`identifier`: `string`, `schedule`: `Monthly`, `functionName`: `Name`, \...`args`: `Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`
  `cron`       \<Name\>(`identifier`: `string`, `cron`: `CronString`, `functionName`: `Name`, \...`args`: `Parameters`\<`NamedSchedulableFunction`\<`API`, `Name`\>\>) =\> `void`

------------------------------------------------------------------------

### GenericDocument​

Ƭ **GenericDocument**: `Record`\<`string`, `Value`\>

A document stored in Convex.

------------------------------------------------------------------------

### GenericFieldPaths​

Ƭ **GenericFieldPaths**: `string`

A type describing all of the document fields in a table.

These can either be field names (like \"name\") or references to fields
on nested objects (like \"properties.name\").

------------------------------------------------------------------------

### GenericIndexFields​

Ƭ **GenericIndexFields**: `string`\[\]

A type describing the ordered fields in an index.

These can either be field names (like \"name\") or references to fields
on nested objects (like \"properties.name\").

------------------------------------------------------------------------

### GenericTableIndexes​

Ƭ **GenericTableIndexes**: `Record`\<`string`, `GenericIndexFields`\>

A type describing the indexes in a table.

It\'s an object mapping each index name to the fields in the index.

------------------------------------------------------------------------

### GenericSearchIndexConfig​

Ƭ **GenericSearchIndexConfig**: `Object`

A type describing the configuration of a search index.

#### Type declaration​

  Name             Type
  ---------------- ----------
  `searchField`    `string`
  `filterFields`   `string`

------------------------------------------------------------------------

### GenericTableSearchIndexes​

Ƭ **GenericTableSearchIndexes**: `Record`\<`string`,
`GenericSearchIndexConfig`\>

A type describing all of the search indexes in a table.

This is an object mapping each index name to the config for the index.

------------------------------------------------------------------------

### FieldTypeFromFieldPath​

Ƭ **FieldTypeFromFieldPath**\<`Document`, `FieldPath`\>: `FieldPath`
extends \`\${infer First}.\${infer Second}\` ? `First` extends keyof
`Document` ? `Document`\[`First`\] extends `GenericDocument` ?
`FieldTypeFromFieldPath`\<`Document`\[`First`\], `Second`\> : `null` :
`null` : `FieldPath` extends keyof `Document` ?
`Document`\[`FieldPath`\] : `null`

The type of a field in a document.

Note that this supports both simple fields like \"name\" and nested
fields like \"properties.name\".

If the field is not present in the document it is considered to be
`null`.

#### Type parameters​

  Name          Type
  ------------- ---------------------------
  `Document`    extends `GenericDocument`
  `FieldPath`   extends `string`

------------------------------------------------------------------------

### GenericTableInfo​

Ƭ **GenericTableInfo**: `Object`

A type describing the document type and indexes in a table.

#### Type declaration​

  Name              Type
  ----------------- -----------------------------
  `document`        `GenericDocument`
  `fieldPaths`      `GenericFieldPaths`
  `indexes`         `GenericTableIndexes`
  `searchIndexes`   `GenericTableSearchIndexes`

------------------------------------------------------------------------

### DocumentByInfo​

Ƭ **DocumentByInfo**\<`TableInfo`\>: `TableInfo`\[`"document"`\]

The type of a document in a table for a given GenericTableInfo.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

------------------------------------------------------------------------

### FieldPaths​

Ƭ **FieldPaths**\<`TableInfo`\>: `TableInfo`\[`"fieldPaths"`\]

The field paths in a table for a given GenericTableInfo.

These can either be field names (like \"name\") or references to fields
on nested objects (like \"properties.name\").

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

------------------------------------------------------------------------

### Indexes​

Ƭ **Indexes**\<`TableInfo`\>: `TableInfo`\[`"indexes"`\]

The database indexes in a table for a given GenericTableInfo.

This will be an object mapping index names to the fields in the index.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

------------------------------------------------------------------------

### IndexNames​

Ƭ **IndexNames**\<`TableInfo`\>: keyof `Indexes`\<`TableInfo`\>

The names of indexes in a table for a given GenericTableInfo.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

------------------------------------------------------------------------

### NamedIndex​

Ƭ **NamedIndex**\<`TableInfo`, `IndexName`\>:
`Indexes`\<`TableInfo`\>\[`IndexName`\]

Extract the fields of an index from a GenericTableInfo by name.

#### Type parameters​

  Name          Type
  ------------- -------------------------------------
  `TableInfo`   extends `GenericTableInfo`
  `IndexName`   extends `IndexNames`\<`TableInfo`\>

------------------------------------------------------------------------

### SearchIndexes​

Ƭ **SearchIndexes**\<`TableInfo`\>: `TableInfo`\[`"searchIndexes"`\]

The search indexes in a table for a given GenericTableInfo.

This will be an object mapping index names to the search index config.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

------------------------------------------------------------------------

### SearchIndexNames​

Ƭ **SearchIndexNames**\<`TableInfo`\>: keyof
`SearchIndexes`\<`TableInfo`\>

The names of search indexes in a table for a given GenericTableInfo.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

------------------------------------------------------------------------

### NamedSearchIndex​

Ƭ **NamedSearchIndex**\<`TableInfo`, `IndexName`\>:
`SearchIndexes`\<`TableInfo`\>\[`IndexName`\]

Extract the fields of an index from a GenericTableInfo by name.

#### Type parameters​

  Name          Type
  ------------- -------------------------------------------
  `TableInfo`   extends `GenericTableInfo`
  `IndexName`   extends `SearchIndexNames`\<`TableInfo`\>

------------------------------------------------------------------------

### GenericDataModel​

Ƭ **GenericDataModel**: `Record`\<`string`, `GenericTableInfo`\>

A type describing the tables in a Convex project.

This is designed to be code generated with `npx convex codegen`.

------------------------------------------------------------------------

### AnyDataModel​

Ƭ **AnyDataModel**: `Object`

A GenericDataModel that considers documents to be `any` and does not
support indexes.

This is the default before a schema is defined.

#### Index signature​

▪ \[tableName: `string`\]: { `document`: `any` ; `fieldPaths`:
`GenericFieldPaths` ; `indexes`: ; `searchIndexes`: }

------------------------------------------------------------------------

### TableNamesInDataModel​

Ƭ **TableNamesInDataModel**\<`DataModel`\>: keyof `DataModel` & `string`

A type of all of the table names defined in a GenericDataModel.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`

------------------------------------------------------------------------

### NamedTableInfo​

Ƭ **NamedTableInfo**\<`DataModel`, `TableName`\>:
`DataModel`\[`TableName`\]

Extract the `TableInfo` for a table in a GenericDataModel by table name.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`
  `TableName`   extends keyof `DataModel`

------------------------------------------------------------------------

### DocumentByName​

Ƭ **DocumentByName**\<`DataModel`, `TableName`\>:
`DataModel`\[`TableName`\]\[`"document"`\]

The type of a document in a GenericDataModel by table name.

#### Type parameters​

  Name          Type
  ------------- ------------------------------------------------
  `DataModel`   extends `GenericDataModel`
  `TableName`   extends `TableNamesInDataModel`\<`DataModel`\>

------------------------------------------------------------------------

### ExpressionOrValue​

Ƭ **ExpressionOrValue**\<`T`\>: `Expression`\<`T`\> \| `T`

An Expression or a constant Value

#### Type parameters​

  Name   Type
  ------ -----------------
  `T`    extends `Value`

------------------------------------------------------------------------

### Cursor​

Ƭ **Cursor**: `string`

An opaque identifier used for paginating a database query.

Cursors are returned from paginate and represent the point of the query
where the page of results ended.

To continue paginating, pass the cursor back into paginate in the
PaginationOptions object to fetch another page of results.

Note: Cursors can only be passed to *exactly* the same database query
that they were generated from. You may not reuse a cursor between
different database queries.

------------------------------------------------------------------------

### MutationCtx​

Ƭ **MutationCtx**\<`DataModel`, `API`\>: `Object`

A set of services for use within Convex mutation functions.

The mutation context is passed as the first argument to any Convex
mutation function run on the server.

If you\'re using code generation, use the `MutationCtx` type in
`convex/_generated/server.d.ts` which is typed for your data model.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`
  `API`         extends `GenericAPI`

#### Type declaration​

  Name          Type
  ------------- ---------------------------------
  `db`          `DatabaseWriter`\<`DataModel`\>
  `auth`        `Auth`
  `storage`     `StorageWriter`
  `scheduler`   `Scheduler`\<`API`\>

------------------------------------------------------------------------

### QueryCtx​

Ƭ **QueryCtx**\<`DataModel`\>: `Object`

A set of services for use within Convex query functions.

The query context is passed as the first argument to any Convex query
function run on the server.

This differs from the MutationCtx because all of the services are
read-only.

If you\'re using code generation, use the `QueryCtx` type in
`convex/_generated/server.d.ts` which is typed for your data model.

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`

#### Type declaration​

  Name        Type
  ----------- ---------------------------------
  `db`        `DatabaseReader`\<`DataModel`\>
  `auth`      `Auth`
  `storage`   `StorageReader`

------------------------------------------------------------------------

### PublicMutation​

Ƭ **PublicMutation**\<`Args`, `Output`\>: `Object`

A mutation function that is part of this app\'s public API.

You can create public mutations by wrapping your function in
mutationGeneric and exporting it.

#### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

#### Type declaration​

  Name              Type
  ----------------- ----------
  `args`            `Args`
  `output`          `Output`
  `isMutation`      `true`
  `isPublic`        `true`
  `isRegistered?`   `true`

------------------------------------------------------------------------

### InternalMutation​

Ƭ **InternalMutation**\<`Args`, `Output`\>: `Object`

A mutation function that can only be called internally by other Convex
functions.

You can create internal mutations by wrapping your function in
internalMutationGeneric and exporting it.

#### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

#### Type declaration​

  Name              Type
  ----------------- ----------
  `args`            `Args`
  `output`          `Output`
  `isMutation`      `true`
  `isInternal`      `true`
  `isRegistered?`   `true`

------------------------------------------------------------------------

### PublicQuery​

Ƭ **PublicQuery**\<`Args`, `Output`\>: `Object`

A query function that is part of this app\'s public API.

You can create public queries by wrapping your function in queryGeneric
and exporting it.

#### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

#### Type declaration​

  Name              Type
  ----------------- ----------
  `args`            `Args`
  `output`          `Output`
  `isQuery`         `true`
  `isPublic`        `true`
  `isRegistered?`   `true`

------------------------------------------------------------------------

### InternalQuery​

Ƭ **InternalQuery**\<`Args`, `Output`\>: `Object`

A query function that can only be called internally by other Convex
functions.

You can create internal queries by wrapping your function in
internalQueryGeneric and exporting it.

#### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

#### Type declaration​

  Name              Type
  ----------------- ----------
  `args`            `Args`
  `output`          `Output`
  `isQuery`         `true`
  `isInternal`      `true`
  `isRegistered?`   `true`

------------------------------------------------------------------------

### PublicAction​

Ƭ **PublicAction**\<`Args`, `Output`\>: `Object`

An action that is part of this app\'s public API.

You can create public action by wrapping your function in actionGeneric
and exporting it.

#### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

#### Type declaration​

  Name              Type
  ----------------- ----------
  `args`            `Args`
  `output`          `Output`
  `isAction`        `true`
  `isPublic`        `true`
  `isRegistered?`   `true`

------------------------------------------------------------------------

### InternalAction​

Ƭ **InternalAction**\<`Args`, `Output`\>: `Object`

An action that can only be called internally by other Convex functions.

You can create internal actions by wrapping your function in
internalActionGeneric and exporting it.

#### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

#### Type declaration​

  Name              Type
  ----------------- ----------
  `args`            `Args`
  `output`          `Output`
  `isAction`        `true`
  `isInternal`      `true`
  `isRegistered?`   `true`

------------------------------------------------------------------------

### PublicHttpEndpoint​

Ƭ **PublicHttpEndpoint**: `Object`

#### Call signature​

▸ (`ctx`, `request`): `Response`

An HTTP endpoint that is part of this app\'s public API.

You can create public HTTP endpoints by wrapping your function in
httpEndpointGeneric and exporting it.

##### Parameters​

  Name        Type
  ----------- ----------------------------
  `ctx`       `HttpEndpointCtx`\<`any`\>
  `request`   `Request`

##### Returns​

`Response`

#### Type declaration​

  Name              Type
  ----------------- --------
  `isHttp`          `true`
  `isRegistered?`   `true`

------------------------------------------------------------------------

### MutationBuilder​

Ƭ **MutationBuilder**\<`DataModel`, `API`\>: \<Args, Output\>(`func`:
(`ctx`: `MutationCtx`\<`DataModel`, `API`\>, \...`args`: `Args`) =\>
`Output`) =\> `PublicMutation`\<`Args`, `Output`\>

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`
  `API`         extends `GenericAPI`

#### Type declaration​

▸ \<`Args`, `Output`\>(`func`): `PublicMutation`\<`Args`, `Output`\>

Internal type helper used by Convex code generation.

Used to give mutationGeneric a type specific to your data model.

##### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

##### Parameters​

  Name     Type
  -------- -------------------------------------------------------------------------------
  `func`   (`ctx`: `MutationCtx`\<`DataModel`, `API`\>, \...`args`: `Args`) =\> `Output`

##### Returns​

`PublicMutation`\<`Args`, `Output`\>

------------------------------------------------------------------------

### InternalMutationBuilder​

Ƭ **InternalMutationBuilder**\<`DataModel`, `API`\>: \<Args,
Output\>(`func`: (`ctx`: `MutationCtx`\<`DataModel`, `API`\>,
\...`args`: `Args`) =\> `Output`) =\> `InternalMutation`\<`Args`,
`Output`\>

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`
  `API`         extends `GenericAPI`

#### Type declaration​

▸ \<`Args`, `Output`\>(`func`): `InternalMutation`\<`Args`, `Output`\>

Internal type helper used by Convex code generation.

Used to give internalMutationGeneric a type specific to your data model.

##### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

##### Parameters​

  Name     Type
  -------- -------------------------------------------------------------------------------
  `func`   (`ctx`: `MutationCtx`\<`DataModel`, `API`\>, \...`args`: `Args`) =\> `Output`

##### Returns​

`InternalMutation`\<`Args`, `Output`\>

------------------------------------------------------------------------

### QueryBuilderForDataModel​

Ƭ **QueryBuilderForDataModel**\<`DataModel`\>: \<Args, Output\>(`func`:
(`ctx`: `QueryCtx`\<`DataModel`\>, \...`args`: `Args`) =\> `Output`) =\>
`PublicQuery`\<`Args`, `Output`\>

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`

#### Type declaration​

▸ \<`Args`, `Output`\>(`func`): `PublicQuery`\<`Args`, `Output`\>

Internal type helper used by Convex code generation.

Used to give queryGeneric a type specific to your data model.

##### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

##### Parameters​

  Name     Type
  -------- ---------------------------------------------------------------------
  `func`   (`ctx`: `QueryCtx`\<`DataModel`\>, \...`args`: `Args`) =\> `Output`

##### Returns​

`PublicQuery`\<`Args`, `Output`\>

------------------------------------------------------------------------

### InternalQueryBuilderForDataModel​

Ƭ **InternalQueryBuilderForDataModel**\<`DataModel`\>: \<Args,
Output\>(`func`: (`ctx`: `QueryCtx`\<`DataModel`\>, \...`args`: `Args`)
=\> `Output`) =\> `InternalQuery`\<`Args`, `Output`\>

#### Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`

#### Type declaration​

▸ \<`Args`, `Output`\>(`func`): `InternalQuery`\<`Args`, `Output`\>

Internal type helper used by Convex code generation.

Used to give internalQueryGeneric a type specific to your data model.

##### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

##### Parameters​

  Name     Type
  -------- ---------------------------------------------------------------------
  `func`   (`ctx`: `QueryCtx`\<`DataModel`\>, \...`args`: `Args`) =\> `Output`

##### Returns​

`InternalQuery`\<`Args`, `Output`\>

------------------------------------------------------------------------

### ActionBuilderForAPI​

Ƭ **ActionBuilderForAPI**\<`API`\>: \<Args, Output\>(`func`: (`ctx`:
`ActionCtx`\<`API`\>, \...`args`: `Args`) =\> `Output`) =\>
`PublicAction`\<`Args`, `Output`\>

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ \<`Args`, `Output`\>(`func`): `PublicAction`\<`Args`, `Output`\>

Internal type helper used by Convex code generation.

Used to give actionGeneric a type specific to your data model.

##### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

##### Parameters​

  Name     Type
  -------- ----------------------------------------------------------------
  `func`   (`ctx`: `ActionCtx`\<`API`\>, \...`args`: `Args`) =\> `Output`

##### Returns​

`PublicAction`\<`Args`, `Output`\>

------------------------------------------------------------------------

### InternalActionBuilderForAPI​

Ƭ **InternalActionBuilderForAPI**\<`API`\>: \<Args, Output\>(`func`:
(`ctx`: `ActionCtx`\<`API`\>, \...`args`: `Args`) =\> `Output`) =\>
`InternalAction`\<`Args`, `Output`\>

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ \<`Args`, `Output`\>(`func`): `InternalAction`\<`Args`, `Output`\>

Internal type helper used by Convex code generation.

Used to give internalActionGeneric a type specific to your data model.

##### Type parameters​

  Name       Type
  ---------- -------------------
  `Args`     extends `any`\[\]
  `Output`   `Output`

##### Parameters​

  Name     Type
  -------- ----------------------------------------------------------------
  `func`   (`ctx`: `ActionCtx`\<`API`\>, \...`args`: `Args`) =\> `Output`

##### Returns​

`InternalAction`\<`Args`, `Output`\>

------------------------------------------------------------------------

### HttpEndpointBuilderForAPI​

Ƭ **HttpEndpointBuilderForAPI**\<`API`\>: (`func`: (`ctx`:
`HttpEndpointCtx`\<`API`\>, `request`: `Request`) =\>
`Promise`\<`Response`\>) =\> `PublicHttpEndpoint`

#### Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

#### Type declaration​

▸ (`func`): `PublicHttpEndpoint`

Internal type helper used by Convex code generation.

Used to give httpEndpointGeneric a type specific to your data model and
functions.

##### Parameters​

  Name     Type
  -------- ---------------------------------------------------------------------------------------
  `func`   (`ctx`: `HttpEndpointCtx`\<`API`\>, `request`: `Request`) =\> `Promise`\<`Response`\>

##### Returns​

`PublicHttpEndpoint`

------------------------------------------------------------------------

### RoutableMethod​

Ƭ **RoutableMethod**: typeof `ROUTABLE_HTTP_METHODS`\[`number`\]

A type representing the methods supported by Convex HTTP endpoints.

HEAD is handled by Convex by running GET and stripping the body. CONNECT
is not supported and will not be supported. TRACE is not supported and
will not be supported.

------------------------------------------------------------------------

### StorageId​

Ƭ **StorageId**: `string`

A reference to a file in storage.

This is used in the StorageReader and StorageWriter which are accessible
in Convex queries and mutations via QueryCtx and MutationCtx
respectively.

------------------------------------------------------------------------

### FileMetadata​

Ƭ **FileMetadata**: `Object`

Metadata for a single file as returned by storage.getMetadata.

#### Type declaration​

  Name            Type                 Description
  --------------- -------------------- ------------------------------------------------------
  `storageId`     `StorageId`          ID for referencing the file (eg. via storage.getUrl)
  `sha256`        `string`             Hex encoded sha256 checksum of file contents
  `size`          `number`             Size of the file in bytes
  `contentType`   `string` \| `null`   ContentType of the file if it was provided on upload

------------------------------------------------------------------------

### WithoutSystemFields​

Ƭ **WithoutSystemFields**\<`Document`\>:
`Expand`\<`BetterOmit`\<`Document`, keyof `SystemFields` \| `"_id"`\>\>

A Convex document with the system fields like `_id` and `_creationTime`
omitted.

#### Type parameters​

  Name         Type
  ------------ ---------------------------
  `Document`   extends `GenericDocument`

## Variables​

### ROUTABLE_HTTP_METHODS​

• `Const` **ROUTABLE_HTTP_METHODS**: readonly \[`"GET"`, `"POST"`,
`"PUT"`, `"DELETE"`, `"OPTIONS"`, `"PATCH"`\]

A list of the methods supported by Convex HTTP endpoints.

HEAD is handled by Convex by running GET and stripping the body. CONNECT
is not supported and will not be supported. TRACE is not supported and
will not be supported.

</div>

</div>

</div>

</div>

</div>
