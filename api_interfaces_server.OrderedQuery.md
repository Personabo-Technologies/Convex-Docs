<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   OrderedQuery

<div>

On this page

</div>

<div>

<div>

# Interface: OrderedQuery\<TableInfo\>

</div>

server.OrderedQuery

A Query with an order that has already been defined.

## Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

## Hierarchy​

-   `AsyncIterable`\<`DocumentByInfo`\<`TableInfo`\>\>

    ↳ **`OrderedQuery`**

    ↳↳ `Query`

## Methods​

### \[asyncIterator\]​

▸ **\[asyncIterator\]**():
`AsyncIterator`\<`DocumentByInfo`\<`TableInfo`\>, `any`, `undefined`\>

#### Returns​

`AsyncIterator`\<`DocumentByInfo`\<`TableInfo`\>, `any`, `undefined`\>

#### Inherited from​

AsyncIterable.\_\_@asyncIterator@878

------------------------------------------------------------------------

### filter​

▸ **filter**(`predicate`): `OrderedQuery`\<`TableInfo`\>

Filter the query output, returning only the values for which `predicate`
evaluates to true.

#### Parameters​

  Name          Type                                                                  Description
  ------------- --------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------
  `predicate`   (`q`: `FilterBuilder`\<`TableInfo`\>) =\> `Expression`\<`boolean`\>   An Expression constructed with the supplied FilterBuilder that specifies which documents to keep.

#### Returns​

`OrderedQuery`\<`TableInfo`\>

-   A new OrderedQuery with the given filter predicate applied.

------------------------------------------------------------------------

### paginate​

▸ **paginate**(`options`):
`Promise`\<`PaginationResult`\<`DocumentByInfo`\<`TableInfo`\>\>\>

Load a page of `n` results and obtain a Cursor for loading more.

Note: If this is called from a reactive query function the number of
results may not match `options.numItems`!

`options.numItems` is only an initial value. After the first invocation,
`paginate` will return all items in the original query range. This
ensures that all pages will remain adjacent and non-overlapping.

#### Parameters​

  Name        Type                  Description
  ----------- --------------------- -----------------------------------------------------------------------------------------------
  `options`   `PaginationOptions`   A PaginationOptions object containing the number of items to load and the cursor to start at.

#### Returns​

`Promise`\<`PaginationResult`\<`DocumentByInfo`\<`TableInfo`\>\>\>

A PaginationResult containing the page of results and a cursor to
continue paginating.

------------------------------------------------------------------------

### collect​

▸ **collect**(): `Promise`\<`DocumentByInfo`\<`TableInfo`\>\[\]\>

Execute the query and return all of the results as an array.

Note: when processing a query with a lot of results, it\'s often better
to use the `Query` as an `AsyncIterable` instead.

#### Returns​

`Promise`\<`DocumentByInfo`\<`TableInfo`\>\[\]\>

-   An array of all of the query\'s results.

------------------------------------------------------------------------

### take​

▸ **take**(`n`): `Promise`\<`DocumentByInfo`\<`TableInfo`\>\[\]\>

Execute the query and return the first `n` results.

#### Parameters​

  Name   Type       Description
  ------ ---------- ------------------------------
  `n`    `number`   The number of items to take.

#### Returns​

`Promise`\<`DocumentByInfo`\<`TableInfo`\>\[\]\>

-   An array of the first `n` results of the query (or less if the query
    doesn\'t have `n` results).

------------------------------------------------------------------------

### first​

▸ **first**(): `Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

Execute the query and return the first result if there is one.

#### Returns​

`Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

-   The first value of the query or `null` if the query returned no
    results.

------------------------------------------------------------------------

### unique​

▸ **unique**(): `Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

Execute the query and return the singular result if there is one.

**`Throws`**

Will throw an error if the query returns more than one result.

#### Returns​

`Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

-   The single result returned from the query or null if none exists.

</div>

</div>

</div>

</div>

</div>
