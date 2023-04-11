<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   Query

<div>

On this page

</div>

<div>

<div>

# Interface: Query\<TableInfo\>

</div>

server.Query

The Query interface allows functions to read values out of the database.

**If you only need to load an object by ID, use `db.get(id)` instead.**

Executing a query consists of calling

1.  (Optional) order to define the order
2.  (Optional) filter to refine the results
3.  A *consumer* method to obtain the results

Queries are lazily evaluated. No work is done until iteration begins, so
constructing and extending a query is free. The query is executed
incrementally as the results are iterated over, so early terminating
also reduces the cost of the query.

It is more efficient to use `filter` expression rather than executing
JavaScript to filter.

  ---------------------------- -------------------------------------------------------------------------
  **Ordering**                 
  `order("asc")`               Define the order of query results.
                               
  **Filtering**                
  `filter(...)`                Filter the query results to only the values that match some condition.
                               
  **Consuming**                Execute a query and return results in different ways.
  `[Symbol.asyncIterator]()`   The query\'s results can be iterated over using a `for await..of` loop.
  `collect()`                  Return all of the results as an array.
  `take(n: number)`            Return the first `n` results as an array.
  `first()`                    Return the first result.
  `unique()`                   Return the only result, and throw if there is more than one result.
  ---------------------------- -------------------------------------------------------------------------

To learn more about how to write queries, see Querying the Database.

## Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

## Hierarchy​

-   `OrderedQuery`\<`TableInfo`\>

    ↳ **`Query`**

    ↳↳ `QueryInitializer`

## Methods​

### \[asyncIterator\]​

▸ **\[asyncIterator\]**():
`AsyncIterator`\<`DocumentByInfo`\<`TableInfo`\>, `any`, `undefined`\>

#### Returns​

`AsyncIterator`\<`DocumentByInfo`\<`TableInfo`\>, `any`, `undefined`\>

#### Inherited from​

OrderedQuery.\[asyncIterator\]

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

#### Overrides​

OrderedQuery.filter

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

OrderedQuery.paginate

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

OrderedQuery.collect

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

OrderedQuery.take

------------------------------------------------------------------------

### first​

▸ **first**(): `Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

Execute the query and return the first result if there is one.

#### Returns​

`Promise`\<`null` \| `DocumentByInfo`\<`TableInfo`\>\>

-   The first value of the query or `null` if the query returned no
    results.

#### Inherited from​

OrderedQuery.first

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

OrderedQuery.unique

</div>

</div>

</div>

</div>

</div>
