<div>

<div>

<div>

<div>

<div>

On this page

</div>

<div>

<div>

# Full Text Search

</div>

**Example:** Search

Full text search allows you to find Convex documents that match given
keywords.

Unlike normal document queries, search queries look *within* a string
field to find the keywords. This can be used to build search features
within your app like searching for messages that contain certain words.

Search queries are automatically reactive, consistent, transactional,
and work seamlessly with pagination. They even include new documents
created with a mutation!

To use full text search you need to:

1.  Define a search index.
2.  Run a search query.

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)Search is
in beta

</div>

<div>

Full text search is currently a beta feature. If you have feedback or
feature requests, let us know on Discord!

</div>

</div>

## Defining search indexes​

Like database indexes, search indexes are a data structure that is built
in advance to enable efficient querying. Search indexes are defined as
part of your Convex schema.

Every search index definition consists of:

1.  A name.
    -   Must be unique per table.
2.  A `searchField`
    -   This is the field which will be indexed for full text search.
    -   It must be of type `string`.
3.  \[Optional\] A list of `filterField`s
    -   These are additional fields that are indexed for fast equality
        filtering within your search index.

To add a search index onto a table, use the `searchIndex` method on your
table\'s schema. For example, if you want an index which can search for
messages matching a keyword in a channel, your schema could look like:

<div>

<div>

convex/schema.ts

</div>

<div>

    import { defineSchema, defineTable, s } from "convex/schema";

    export default defineSchema({
      messages: defineTable({
        body: s.string(),
        channel: s.string(),
      }).searchIndex("search_body", {
        searchField: "body",
        filterFields: ["channel"],
      }),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

You can specify search and filter fields on nested documents by using a
dot-separated path like `properties.name`.

## Running search queries​

A query for \"10 messages in channel \'#general\' that have \'hello\' or
\'hi\' in their body\" would look like:

<div>

<div>

    const messages = await db
      .query("messages")
      .withSearchIndex("search_body", q =>
        q.search("body", "hello hi").eq("channel", "#general")
      )
      .take(10);

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This is just a normal database read that begins by querying the search
index!

The `.withSearchIndex` method defines which search index to query and
how Convex will use that search index to select documents. The first
argument is the name of the index and the second is a *search filter
expression*. A search filter expression is a description of which
documents Convex should consider when running the query.

A search filter expression is always a chained list of:

1.  1 search expression against the index\'s search field defined with
    `.search`.
2.  0 or more equality expressions against the index\'s filter fields
    defined with `.eq`.

### Search expressions​

Internally, Convex will break up the search expression\'s query into
separate words (called *terms*) and search for any of them within the
field.

In the example above, the expression `search("body", "hello hi")` would
internally be split into `"hi"` and `"hello"` and compared against the
terms in your document (ignoring case and punctuation). This matches:

-   `"hi"`
-   `"Sujay, hello!"`
-   `"oh HI there"`
-   \...

### Equality expressions​

Unlike search expressions, equality expressions will filter to only
documents that have an exact match in the given field. In the example
above, `eq("channel", "#general")` will only match documents that have
exactly `"#general"` in their `channel` field.

Equality expressions support fields of any type (not just text).

### Other filtering​

Because search queries are normal database queries, you can also filter
results using the `.filter` method!

Here\'s a query for \"messages containing \'hi\' sent in the last 10
minutes\":

<div>

<div>

    const messages = await db
      .query("messages")
      .withSearchIndex("search_body", q => q.search("body", "hi"))
      .filter(q => q.gt(q.field("_creationTime", Date.now() - 10 * 60000)))
      .take(10);

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

**For performance, always put as many of your filters as possible into
`.withSearchIndex`.**

Every search query is executed by:

1.  First, querying the search index using the search filter expression
    in `withSearchIndex`.
2.  Then, filtering the results one-by-one using any additional `filter`
    expressions.

Having a very specific search filter expression will make your query
faster and less likely to hit Convex\'s limits because Convex will use
the search index to efficiently cut down on the number of results to
consider.

### Retrieving results and paginating​

Just like ordinary database queries, you can retrieve the results using
`.collect()`, `.take(n)`, `.first()`, and `.unique()`.

Additionally, search results can be paginated using `.paginate(opts)`.

Note that `collect()` will throw an exception if it attempts to collect
more than the limit of 1024 documents. It is often better to pick a
smaller limit and use `take(n)` or paginate the results.

### Relevance order​

Search queries always return results in relevance order based on how
well the document matches the search text.

Internally, Convex ranks documents based on their BM25 score which takes
into account:

-   How many words in the search query appear in the field?
-   How many times do they appear?
-   How long is the text field?

If multiple documents have the same score, the newest documents are
returned first.

## Limits​

Search indexes must have:

-   Exactly 1 search field.
-   Up to 16 filter fields.

Search indexes count against the limit of 32 indexes per table.

Search queries can have:

-   Up to 16 terms (words) in the search expression.
-   Up to 8 filter expressions.

Additionally, search queries can scan up to 1024 results from the search
index.

## Coming soon​

We plan to expand Convex full text search to include:

-   Prefix search/typeahead support
-   Snippeting (returning the matched positions in the search text)
-   Faceted search (counting the number of results per filter field
    value)
-   Typo tolerance/fuzzy search
-   Additional languages
-   Searching across multiple fields

If any of these features is important for your app, let us know on
Discord!

</div>

</div>

</div>

</div>

</div>
