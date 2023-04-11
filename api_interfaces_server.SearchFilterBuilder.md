<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   SearchFilterBuilder

<div>

On this page

</div>

<div>

<div>

# Interface: SearchFilterBuilder\<Document, SearchIndexConfig\>

</div>

server.SearchFilterBuilder

Builder for defining search filters.

A search filter is a chained list of:

1.  One search expression constructed with `.search`.
2.  Zero or more equality expressions constructed with `.eq`.

The search expression must search for text in the index\'s
`searchField`. The filter expressions can use any of the `filterFields`
defined in the index.

For all other filtering use filter.

To learn about full text search, see Indexes.

## Type parameters​

  Name                  Type
  --------------------- ------------------------------------
  `Document`            extends `GenericDocument`
  `SearchIndexConfig`   extends `GenericSearchIndexConfig`

## Methods​

### search​

▸ **search**(`fieldName`, `query`): `SearchFilterFinalizer`\<`Document`,
`SearchIndexConfig`\>

Search for the terms in `query` within `doc[fieldName]`.

This will do a full text search that returns results where any word of
of `query` appears in the field.

Documents will be returned based on their relevance to the query. This
takes into account:

-   How many words in the query appear in the text?
-   How many times do they appear?
-   How long is the text field?

#### Parameters​

  Name          Type                                     Description
  ------------- ---------------------------------------- ----------------------------------------------------------------------------------------
  `fieldName`   `SearchIndexConfig`\[`"searchField"`\]   The name of the field to search in. This must be listed as the index\'s `searchField`.
  `query`       `string`                                 The query text to search for.

#### Returns​

`SearchFilterFinalizer`\<`Document`, `SearchIndexConfig`\>

</div>

</div>

</div>

</div>

</div>
