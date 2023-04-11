<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   QueryInitializer

<div>

On this page

</div>

<div>

<div>

# Interface: QueryInitializer\<TableInfo\>

</div>

server.QueryInitializer

The QueryInitializer interface is the entry point for building a Query
over a Convex database table.

There are two types of queries:

1.  Full table scans: Queries created with fullTableScan which iterate
    over all of the documents in the table in insertion order.
2.  Indexed Queries: Queries created with withIndex which iterate over
    an index range in index order.

For convenience, QueryInitializer extends the Query interface,
implicitly starting a full table scan.

## Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

## Hierarchy​

-   `Query`\<`TableInfo`\>

    ↳ **`QueryInitializer`**

## Methods​

### \[asyncIterator\]​

▸ **\[asyncIterator\]**():
`AsyncIterator`\<`DocumentByInfo`\<`TableInfo`\>, `any`, `undefined`\>

#### Returns​

`AsyncIterator`\<`DocumentByInfo`\<`TableInfo`\>, `any`, `undefined`\>

#### Inherited from​

Query.\[asyncIterator\]

------------------------------------------------------------------------

### fullTableScan​

▸ **fullTableScan**(): `Query`\<`TableInfo`\>

Query by reading all of the values out of this table.

This query\'s cost is relative to the size of the entire table, so this
should only be used on tables that will stay very small (say between a
few hundred and a few thousand documents) and are updated infrequently.

#### Returns​

`Query`\<`TableInfo`\>

-   The Query that iterates over every document of the table.

------------------------------------------------------------------------

### withIndex​

▸ **withIndex**\<`IndexName`\>(`indexName`, `indexRange?`):
`Query`\<`TableInfo`\>

Query by reading documents from an index on this table.

This query\'s cost is relative to the number of documents that match the
index range expression.

Results will be returned in index order.

To learn about indexes, see Indexes.

#### Type parameters​

  Name          Type
  ------------- ------------------------------------------
  `IndexName`   extends `string` \| `number` \| `symbol`

#### Parameters​

  Name            Type                                                                                                                            Description
  --------------- ------------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `indexName`     `IndexName`                                                                                                                     The name of the index to query.
  `indexRange?`   (`q`: `IndexRangeBuilder`\<`DocumentByInfo`\<`TableInfo`\>, `NamedIndex`\<`TableInfo`, `IndexName`\>, `0`\>) =\> `IndexRange`   An optional index range constructed with the supplied IndexRangeBuilder. An index range is a description of which documents Convex should consider when running the query. If no index range is present, the query will consider all documents in the index.

#### Returns​

`Query`\<`TableInfo`\>

-   The query that yields documents in the index.

------------------------------------------------------------------------

### withSearchIndex​

▸ **withSearchIndex**\<`IndexName`\>(`indexName`, `searchFilter`):
`OrderedQuery`\<`TableInfo`\>

Query by running a full text search against a search index.

Search queries must always search for some text within the index\'s
`searchField`. This query can optionally add equality filters for any
`filterFields` specified in the index.

Documents will be returned in relevance order based on how well they
match the search text.

To learn about full text search, see Indexes.

#### Type parameters​

  Name          Type
  ------------- ------------------------------------------
  `IndexName`   extends `string` \| `number` \| `symbol`

#### Parameters​

  Name             Type                                                                                                                                 Description
  ---------------- ------------------------------------------------------------------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `indexName`      `IndexName`                                                                                                                          The name of the search index to query.
  `searchFilter`   (`q`: `SearchFilterBuilder`\<`DocumentByInfo`\<`TableInfo`\>, `NamedSearchIndex`\<`TableInfo`, `IndexName`\>\>) =\> `SearchFilter`   A search filter expression constructed with the supplied SearchFilterBuilder. This defines the full text search to run along with equality filtering to run within the search index.

#### Returns​

`OrderedQuery`\<`TableInfo`\>

-   A query that searches for matching documents, returning them in
    relevancy order.

------------------------------------------------------------------------

### filter​

▸ **filter**(`predicate`): `Query`\<`TableInfo`\>

Filter the query output, returning only the values for which `predicate`
evaluates to true.

#### Parameters​

  Name          Type                                                                  Description
  ------------- --------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------
  `predicate`   (`q`: `FilterBuilder`\<`TableInfo`\>) =\> `Expression`\<`boolean`\>   An Expression constructed with the supplied FilterBuilder that specifies which documents to keep.

#### Returns​

`Query`\<`TableInfo`\>

-   A new Query with the given filter predicate applied.

#### Inherited from​

Query.filter

------------------------------------------------------------------------

### order​

▸ **order**(`order`): `OrderedQuery`\<`TableInfo`\>

Define the order of the query output.

Use `"asc"` for an ascending order and `"desc"` for a descending order.
If not specified, the order defaults to ascending.

#### Parameters​

  Name      Type                  Description
  --------- --------------------- ---------------------------------
  `order`   `"asc"` \| `"desc"`   The order to return results in.

#### Returns​

`OrderedQuery`\<`TableInfo`\>

#### Inherited from​

Query.order

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

#### Inherited from​

Query.paginate

------------------------------------------------------------------------

### collect​

▸ **collect**(): `Promise`\<`DocumentByInfo`\<`TableInfo`\>\[\]\>

Execute the query and return all of the results as an array.

Note: when processing a query with a lot of results, it\'s often better
to use the `Query` as an `AsyncIterable` instead.

#### Returns​

`Promise`\<`DocumentByInfo`\<`TableInfo`\>\[\]\>

-   An array of all of the query\'s results.

#### Inherited from​

Query.collect

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

#### Inherited from​

Query.take

------------------------------------------------------------------------

### first​

▸ **first**(): `Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

Execute the query and return the first result if there is one.

#### Returns​

`Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

-   The first value of the query or `null` if the query returned no
    results.

#### Inherited from​

Query.first

------------------------------------------------------------------------

### unique​

▸ **unique**(): `Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

Execute the query and return the singular result if there is one.

**`Throws`**

Will throw an error if the query returns more than one result.

#### Returns​

`Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

-   The single result returned from the query or null if none exists.

#### Inherited from​

Query.unique

</div>

</div>

</div>

</div>

</div>
