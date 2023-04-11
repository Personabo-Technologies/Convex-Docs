<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/browser
-   OptimisticLocalStore

<div>

On this page

</div>

<div>

<div>

# Interface: OptimisticLocalStore\<API\>

</div>

browser.OptimisticLocalStore

A view of the query results currently in the Convex client for use
within optimistic updates.

## Type parameters​

  Name    Type
  ------- -------------------------------------
  `API`   extends `GenericAPI` = `GenericAPI`

## Methods​

### getQuery​

▸ **getQuery**\<`Name`\>(`name`, `args`): `undefined` \|
`ReturnType`\<`NamedQuery`\<`API`, `Name`\>\>

Retrieve the result of a query from the client.

Important: Query results should be treated as immutable! Always make new
copies of structures within query results to avoid corrupting data
within the client.

#### Type parameters​

  Name     Type
  -------- ------------------
  `Name`   extends `string`

#### Parameters​

  Name     Type                                            Description
  -------- ----------------------------------------------- -------------------------------------------
  `name`   `Name`                                          The name of the query.
  `args`   `Parameters`\<`NamedQuery`\<`API`, `Name`\>\>   An array of the arguments for this query.

#### Returns​

`undefined` \| `ReturnType`\<`NamedQuery`\<`API`, `Name`\>\>

The query result or `undefined` if the query is not currently in the
client.

------------------------------------------------------------------------

### getAllQueries​

▸ **getAllQueries**\<`Name`\>(`name`): { `args`:
`Parameters`\<`NamedQuery`\<`API`, `Name`\>\> ; `value`: `undefined` \|
`ReturnType`\<`NamedQuery`\<`API`, `Name`\>\> }\[\]

Retrieve the results are arguments of all queries with a given name.

This is useful for complex optimistic updates that need to inspect and
update many query results (for example updating a paginated list).

Important: Query results should be treated as immutable! Always make new
copies of structures within query results to avoid corrupting data
within the client.

#### Type parameters​

  Name     Type
  -------- ------------------
  `Name`   extends `string`

#### Parameters​

  Name     Type     Description
  -------- -------- ------------------------
  `name`   `Name`   The name of the query.

#### Returns​

{ `args`: `Parameters`\<`NamedQuery`\<`API`, `Name`\>\> ; `value`:
`undefined` \| `ReturnType`\<`NamedQuery`\<`API`, `Name`\>\> }\[\]

An array of objects, one for each query of the given name. Each object
includes:

-   `args` - An array of the arguments to the query.
-   `value` The query result or `undefined` if the query is loading.

------------------------------------------------------------------------

### setQuery​

▸ **setQuery**\<`Name`\>(`name`, `args`, `value`): `void`

Optimistically update the result of a query.

This can either be a new value (perhaps derived from the old value from
getQuery) or `undefined` to remove the query. Removing a query is useful
to create loading states while Convex recomputes the query results.

#### Type parameters​

  Name     Type
  -------- ------------------
  `Name`   extends `string`

#### Parameters​

  Name      Type                                                           Description
  --------- -------------------------------------------------------------- --------------------------------------------------------------------------------
  `name`    `Name`                                                         The name of the query.
  `args`    `Parameters`\<`NamedQuery`\<`API`, `Name`\>\>                  An array of the arguments for this query.
  `value`   `undefined` \| `ReturnType`\<`NamedQuery`\<`API`, `Name`\>\>   The new value to set the query to or `undefined` to remove it from the client.

#### Returns​

`void`

</div>

</div>

</div>

</div>

</div>
