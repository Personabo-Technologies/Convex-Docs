<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/react
-   Watch

<div>

On this page

</div>

<div>

<div>

# Interface: Watch\<T\>

</div>

react.Watch

A watch on the output of a Convex query function.

## Type parameters​

  Name
  ------
  `T`

## Methods​

### onUpdate​

▸ **onUpdate**(`callback`): () =\> `void`

Initiate a watch on the output of a query.

This will subscribe to this query and call the callback whenever the
query result changes.

**Important: If the query is already known on the client this watch will
never be invoked.** To get the current, local result call
localQueryResult.

#### Parameters​

  Name         Type            Description
  ------------ --------------- ------------------------------------------------------------
  `callback`   () =\> `void`   Function that is called whenever the query result changes.

#### Returns​

`fn`

-   A function that disposes of the subscription.

▸ (): `void`

Initiate a watch on the output of a query.

This will subscribe to this query and call the callback whenever the
query result changes.

**Important: If the query is already known on the client this watch will
never be invoked.** To get the current, local result call
localQueryResult.

##### Returns​

`void`

-   A function that disposes of the subscription.

------------------------------------------------------------------------

### localQueryResult​

▸ **localQueryResult**(): `undefined` \| `T`

Get the current result of a query.

This will only return a result if we\'re already subscribed to the query
and have received a result from the server or the query value has been
set optimistically.

**`Throws`**

An error if the query encountered an error on the server.

#### Returns​

`undefined` \| `T`

The result of the query or `undefined` if it isn\'t known.

------------------------------------------------------------------------

### journal​

▸ **journal**(): `undefined` \| `QueryJournal`

Get the current QueryJournal for this query.

If we have not yet received a result for this query, this will be
`undefined`.

#### Returns​

`undefined` \| `QueryJournal`

</div>

</div>

</div>

</div>

</div>
