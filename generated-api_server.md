<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Generated Code
-   server.js

<div>

On this page

</div>

<div>

<div>

# server.js

</div>

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)This code
is generated

</div>

<div>

These exports are not directly available in the `convex` package!

Instead you must run `npx convex codegen` to create
`convex/_generated/server.js` and `convex/_generated/server.d.ts`.

</div>

</div>

Generated utilities for implementing server-side Convex query and
mutation functions.

## Functions​

### query​

▸ **query**(`func`): `PublicQuery`

Define a query in this Convex app\'s public API.

This function will be allowed to read your Convex database and will be
accessible from the client.

This is an alias of `queryGeneric` that is typed for your app\'s data
model.

#### Parameters​

  Name     Description
  -------- -------------------------------------------------------------------
  `func`   The query function. It receives a QueryCtx as its first argument.

#### Returns​

`PublicQuery`

The wrapped query. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### internalQuery​

▸ **internalQuery**(`func`): `InternalQuery`

Define a query that is only accessible from other Convex functions (but
not from the client).

This function will be allowed to read from your Convex database. It will
not be accessible from the client.

This is an alias of `internalQueryGeneric` that is typed for your app\'s
data model.

#### Parameters​

  Name     Description
  -------- -------------------------------------------------------------------
  `func`   The query function. It receives a QueryCtx as its first argument.

#### Returns​

`InternalQuery`

The wrapped query. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### mutation​

▸ **mutation**(`func`): `PublicMutation`

Define a mutation in this Convex app\'s public API.

This function will be allowed to modify your Convex database and will be
accessible from the client.

This is an alias of `mutationGeneric` that is typed for your app\'s data
model.

#### Parameters​

  Name     Description
  -------- -------------------------------------------------------------------------
  `func`   The mutation function. It receives a MutationCtx as its first argument.

#### Returns​

`PublicMutation`

The wrapped mutation. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### internalMutation​

▸ **internalMutation**(`func`): `InternalMutation`

Define a mutation that is only accessible from other Convex functions
(but not from the client).

This function will be allowed to read and write from your Convex
database. It will not be accessible from the client.

This is an alias of `internalMutationGeneric` that is typed for your
app\'s data model.

#### Parameters​

  Name     Description
  -------- -------------------------------------------------------------------------
  `func`   The mutation function. It receives a MutationCtx as its first argument.

#### Returns​

`InternalMutation`

The wrapped mutation. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### action​

▸ **action**(`func`): `PublicAction`

Define an action in this Convex app\'s public API.

An action is a function which can execute any JavaScript code, including
non-deterministic code and code with side-effects. Actions are often
used to call into third-party services. Actions execute in a Node.js
environment and can interact with the database indirectly by calling
queries and mutations via the provided `ActionCtx` object. Actions need
to be defined in the `/convex/actions` directory. Queries and mutations,
on the other hand, must be defined outside of the `/convex/actions`
directory.

This is an alias of `actionGeneric` that is typed for your app\'s data
model.

#### Parameters​

  Name     Description
  -------- ---------------------------------------------------------------------
  `func`   The action function. It receives a ActionCtx as its first argument.

#### Returns​

`PublicAction`

The wrapped function. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### internalAction​

▸ **internalAction**(`func`): `InternalAction`

Define an action that is only accessible from other Convex functions
(but not from the client).

This is an alias of `internalActionGeneric` that is typed for your
app\'s data model.

#### Parameters​

  Name     Description
  -------- ---------------------------------------------------------------------
  `func`   The action function. It receives a ActionCtx as its first argument.

#### Returns​

`InternalAction`

The wrapped action. Include this as an `export` to name it and make it
accessible.

------------------------------------------------------------------------

### httpEndpoint​

▸
**httpEndpoint**(`func: (ctx: HttpEndpointCtx, request: Request) => Promise<Response>`):
`PublicHttpEndpoint`

#### Parameters​

  Name     Type                                                              Description
  -------- ----------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------
  `func`   `(ctx: HttpEndpointCtx, request: Request) => Promise<Response>`   The endpoint function. It receives a `HttpEndpointCtx` as its first argument and a `Request` as its second argument.

#### Returns​

`PublicHttpEndpoint`

The wrapped endpoint function. Import this function from
`convex/http.js` and route it to hook it up.

## Types​

### QueryCtx​

Ƭ **QueryCtx**: `Object`

A set of services for use within Convex query functions.

The query context is passed as the first argument to any Convex query
function run on the server.

This differs from the MutationCtx because all of the services are
read-only.

This is an alias of `QueryCtx` that is typed for your app\'s data model.

#### Type declaration​

  Name        Type
  ----------- ------------------
  `db`        `DatabaseReader`
  `auth`      `Auth`
  `storage`   `StorageReader`

------------------------------------------------------------------------

### MutationCtx​

Ƭ **MutationCtx**: `Object`

A set of services for use within Convex mutation functions.

The mutation context is passed as the first argument to any Convex
mutation function run on the server.

This is an alias of `MutationCtx` that is typed for your app\'s data
model.

#### Type declaration​

  Name          Type
  ------------- ------------------
  `db`          `DatabaseWriter`
  `auth`        `Auth`
  `storage`     `StorageWriter`
  `scheduler`   `Scheduler`

------------------------------------------------------------------------

### ActionCtx​

Ƭ **ActionCtx**: `Object`

A set of services for use within Convex action functions.

The action context is passed as the first argument to any Convex action
function run on the server.

This is an alias of `ActionCtx` that is typed for your app\'s data
model.

#### Type declaration​

  Name            Type
  --------------- ----------------------------------------------------------------
  `runQuery`      (`name`: `string`, \...`args`: `Value[]`) =\> `Promise<Value>`
  `runMutation`   (`name`: `string`, \...`args`: `Value[]`) =\> `Promise<Value>`
  `auth`          `Auth`
  `scheduler`     `Scheduler`

------------------------------------------------------------------------

### HttpEndpointCtx​

Ƭ **HttpEndpointCtx**: `Object`

A set of services for use within Convex HTTP endpoints.

The HttpEndpointCtx is passed as the first argument to any Convex HTTP
endpoint run on the server.

This is an alias of `HttpEndpointCtx` that is typed for your app\'s API.

#### Type declaration​

  Name            Type
  --------------- ----------------------------------------------------------------
  `runQuery`      (`name`: `string`, \...`args`: `Value[]`) =\> `Promise<Value>`
  `runMutation`   (`name`: `string`, \...`args`: `Value[]`) =\> `Promise<Value>`
  `runAction`     (`name`: `string`, \...`args`: `Value[]`) =\> `Promise<Value>`
  `auth`          `Auth`
  `storage`       `StorageHttpWriter`

------------------------------------------------------------------------

### DatabaseReader​

An interface to read from the database within Convex query functions.

This is an alias of `DatabaseReader` that is typed for your app\'s data
model.

------------------------------------------------------------------------

### DatabaseWriter​

An interface to read from and write to the database within Convex
mutation functions.

This is an alias of `DatabaseWriter` that is typed for your app\'s data
model.

</div>

</div>

</div>

</div>

</div>
