<div>

<div>

<div>

<div>

-   Home
-   Database
-   Paginated Queries

<div>

On this page

</div>

<div>

<div>

# Paginated Queries

</div>

**Example:** Pagination

Paginated queries are queries that return a list of results in
incremental pages.

This can be used to build components with \"Load More\" buttons or
\"infinite scroll\" UIs where more results are loaded as the user
scrolls.

Using pagination in Convex is as simple as:

1.  Writing a paginated query function that calls `.paginate(opts)`.
2.  Using the `usePaginatedQuery` React hook.

Like other Convex queries, paginated queries are completely reactive.

## Writing Paginated Query Functions​

Convex uses cursor-based pagination. This means that paginated queries
return a string called a `Cursor` that represents the point in the
results that the current page ended. To load more results, you simply
call the query function again, passing in the cursor.

To build this in Convex, define a query function that:

1.  Takes `PaginationOptions` as its first argument.
    -   This is an object with `numItems` and `cursor` fields.
    -   You may include additional arguments as well.
2.  Calls `.paginate(opts)` on a database query, passing in the
    `PaginationOptions` and returning its result.
    -   The returned `page` in the `PaginationResult` is an array of
        documents. You may `map` or `filter` it before returning it.

<div>

<div>

convex/listMessages.js

</div>

<div>

    import { query } from "./_generated/server";

    export default query(async ({ db }, opts) => {
      return await db.query("messages").order("desc").paginate(opts);
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Paginating within React Components​

To paginate within a React component, use the `usePaginatedQuery` hook.
This hook gives you a simple interface for rendering the current items
and requesting more. Internally, this hook manages the continuation
cursors.

The arguments to this hook are:

-   The name of the paginated query function.
-   An options object with the `initialNumItems` to load on the first
    page.
-   Any additional arguments that the query function expects.

The hook returns an object with:

-   `results`: An array of the currently loaded results.
-   `status`: The status of the pagination. The possible statuses are:
    -   `"CanLoadMore"`: This query may have more items to fetch. Call
        `loadMore` to fetch another page.
    -   `"LoadingMore"`: We\'re currently loading another page of
        results.
    -   `"Exhausted"`: We\'ve paginated to the end of the list.
-   `loadMore(n)`: A callback to fetch more results. This will be
    `undefined` unless the status is `"CanLoadMore"`.

<div>

<div>

    const { results, status, loadMore } = usePaginatedQuery("listMessages", {
      initialNumItems: 5,
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Reactivity​

Like any other Convex query functions, paginated queries are
**completely reactive**. Your React components will automatically
rerender if items in your paginated list are added, removed or changed.

One consequence of this is that **page sizes in Convex may change!** If
you request a page of 10 items and then one item is removed, this page
may \"shrink\" to only have 9 items. Similarly if new items are added, a
page may \"grow\" beyond its initial size.

</div>

</div>

</div>

</div>

</div>
