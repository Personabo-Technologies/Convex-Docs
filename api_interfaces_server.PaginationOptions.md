<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   PaginationOptions

<div>

On this page

</div>

<div>

<div>

# Interface: PaginationOptions

</div>

server.PaginationOptions

The options passed to paginate.

## Properties​

### numItems​

• **numItems**: `number`

Number of items to load in this page of results.

Note: This is only an initial value!

If you are running this paginated query in a reactive query function,
you may receive more or less items than this if items were added to or
removed from the query range.

------------------------------------------------------------------------

### cursor​

• **cursor**: `null` \| `string`

A Cursor representing the start of this page or `null` to start at the
beginning of the query results.

</div>

</div>

</div>

</div>

</div>
