<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/schema
-   SearchIndexConfig

<div>

On this page

</div>

<div>

<div>

# Interface: SearchIndexConfig\<SearchField, FilterFields\>

</div>

schema.SearchIndexConfig

The configuration for a search index.

## Type parameters​

  Name             Type
  ---------------- ------------------
  `SearchField`    extends `string`
  `FilterFields`   extends `string`

## Properties​

### searchField​

• **searchField**: `SearchField`

The field to index for full text search.

This must be a field of type `string`.

------------------------------------------------------------------------

### filterFields​

• `Optional` **filterFields**: `FilterFields`\[\]

Additional fields to index for fast filtering when running search
queries.

</div>

</div>

</div>

</div>

</div>
