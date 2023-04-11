<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/browser
-   InternalConvexClient

<div>

On this page

</div>

<div>

<div>

# Class: InternalConvexClient

</div>

browser.InternalConvexClient

Low-level client for directly integrating state management libraries
with Convex.

Most developers should use higher level clients, like the
ConvexHttpClient or the React hook based ConvexReactClient.

## Constructors​

### constructor​

• **new InternalConvexClient**(`address`, `onTransition`, `options?`)

#### Parameters​

  Name             Type                                          Description
  ---------------- --------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------
  `address`        `string`                                      The url of your Convex deployment, often provided by an environment variable. E.g. `https://small-mouse-123.convex.cloud`.
  `onTransition`   (`updatedQueries`: `string`\[\]) =\> `void`   A callback receiving an array of query tokens corresponding to query results that have changed.
  `options?`       `ClientOptions`                               See ClientOptions for a full description.

## Methods​

### setAuth​

▸ **setAuth**(`fetchToken`): `Promise`\<`void`\>

#### Parameters​

  Name           Type
  -------------- --------------------
  `fetchToken`   `AuthTokenFetcher`

#### Returns​

`Promise`\<`void`\>

------------------------------------------------------------------------

### hasAuth​

▸ **hasAuth**(): `boolean`

#### Returns​

`boolean`

------------------------------------------------------------------------

### clearAuth​

▸ **clearAuth**(): `void`

#### Returns​

`void`

------------------------------------------------------------------------

### subscribe​

▸ **subscribe**(`name`, `args`, `journal?`): `Object`

Subscribe to a query function.

Whenever this query\'s result changes, the `onTransition` callback
passed into the constructor will be called.

#### Parameters​

  Name         Type             Description
  ------------ ---------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `name`       `string`         The name of the query.
  `args`       `any`\[\]        An array of the arguments to the query.
  `journal?`   `QueryJournal`   An (optional) journal produced from a previous execution of this query function. Note that if this query function with these arguments has already been requested the journal will have no effect.

#### Returns​

`Object`

An object containing a QueryToken corresponding to this query and an
`unsubscribe` callback.

  Name            Type
  --------------- ---------------
  `queryToken`    `string`
  `unsubscribe`   () =\> `void`

------------------------------------------------------------------------

### localQueryResult​

▸ **localQueryResult**(`udfPath`, `args`): `undefined` \| `Value`

A query result based only on the current, local state.

The only way this will return a value is if we\'re already subscribed to
the query or its value has been set optimistically.

#### Parameters​

  Name        Type
  ----------- -----------
  `udfPath`   `string`
  `args`      `any`\[\]

#### Returns​

`undefined` \| `Value`

------------------------------------------------------------------------

### queryJournal​

▸ **queryJournal**(`name`, `args`): `undefined` \| `QueryJournal`

Retrieve the current QueryJournal for this query function.

If we have not yet received a result for this query, this will be
`undefined`.

#### Parameters​

  Name     Type        Description
  -------- ----------- --------------------------------------
  `name`   `string`    The name of the query.
  `args`   `any`\[\]   An array of arguments to this query.

#### Returns​

`undefined` \| `QueryJournal`

The query\'s QueryJournal or `undefined`.

------------------------------------------------------------------------

### connectionState​

▸ **connectionState**(): `ConnectionState`

Get the current ConnectionState between the client and the Convex
backend.

#### Returns​

`ConnectionState`

The ConnectionState with the Convex backend.

------------------------------------------------------------------------

### mutate​

▸ **mutate**\<`Args`\>(`udfPath`, `args`, `optimisticUpdate?`):
`Promise`\<`any`\>

#### Type parameters​

  Name     Type
  -------- -------------------
  `Args`   extends `any`\[\]

#### Parameters​

  Name                 Type                                                   Default value
  -------------------- ------------------------------------------------------ ---------------
  `udfPath`            `string`                                               `undefined`
  `args`               `Args`                                                 `undefined`
  `optimisticUpdate`   `null` \| `OptimisticUpdate`\<`GenericAPI`, `Args`\>   `null`

#### Returns​

`Promise`\<`any`\>

------------------------------------------------------------------------

### action​

▸ **action**\<`Args`\>(`udfPath`, `args`): `Promise`\<`any`\>

#### Type parameters​

  Name     Type
  -------- -------------------
  `Args`   extends `any`\[\]

#### Parameters​

  Name        Type
  ----------- ----------
  `udfPath`   `string`
  `args`      `Args`

#### Returns​

`Promise`\<`any`\>

------------------------------------------------------------------------

### close​

▸ **close**(): `Promise`\<`void`\>

#### Returns​

`Promise`\<`void`\>

</div>

</div>

</div>

</div>

</div>
