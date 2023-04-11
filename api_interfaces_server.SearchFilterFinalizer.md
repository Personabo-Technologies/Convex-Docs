<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   SearchFilterFinalizer

<div>

On this page

</div>

<div>

<div>

# Interface: SearchFilterFinalizer\<Document, SearchIndexConfig\>

</div>

server.SearchFilterFinalizer

Builder to define equality expressions as part of a search filter.

See SearchFilterBuilder.

## Type parameters​

  Name                  Type
  --------------------- ------------------------------------
  `Document`            extends `GenericDocument`
  `SearchIndexConfig`   extends `GenericSearchIndexConfig`

## Hierarchy​

-   `SearchFilter`

    ↳ **`SearchFilterFinalizer`**

## Methods​

### eq​

▸ **eq**\<`FieldName`\>(`fieldName`, `value`):
`SearchFilterFinalizer`\<`Document`, `SearchIndexConfig`\>

Restrict this query to documents where `doc[fieldName] === value`.

#### Type parameters​

  Name          Type
  ------------- ------------------
  `FieldName`   extends `string`

#### Parameters​

  Name          Type                                                  Description
  ------------- ----------------------------------------------------- ----------------------------------------------------------------------------------------------
  `fieldName`   `FieldName`                                           The name of the field to compare. This must be listed in the search index\'s `filterFields`.
  `value`       `FieldTypeFromFieldPath`\<`Document`, `FieldName`\>   The value to compare against.

#### Returns​

`SearchFilterFinalizer`\<`Document`, `SearchIndexConfig`\>

</div>

</div>

</div>

</div>

</div>
