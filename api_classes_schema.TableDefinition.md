<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/schema
-   TableDefinition

<div>

On this page

</div>

<div>

<div>

# Class: TableDefinition\<Document, FieldPaths, Indexes, SearchIndexes\>

</div>

schema.TableDefinition

The definition of a table within a schema.

This should be produced by using defineTable.

## Type parameters​

  Name              Type
  ----------------- -----------------------------------------------
  `Document`        extends `GenericDocument` = `GenericDocument`
  `FieldPaths`      extends `string` = `string`
  `Indexes`         extends `GenericTableIndexes` =
  `SearchIndexes`   extends `GenericTableSearchIndexes` =

## Methods​

### index​

▸ **index**\<`IndexName`, `FirstFieldPath`, `RestFieldPaths`\>(`name`,
`fields`): `TableDefinition`\<`Document`, `FieldPaths`,
`Expand`\<`Indexes` & `Record`\<`IndexName`, \[`FirstFieldPath`,
\...RestFieldPaths\[\], `"_creationTime"`\]\>\>, `SearchIndexes`\>

Define an index on this table.

To learn about indexes, see Defining Indexes.

#### Type parameters​

  Name               Type
  ------------------ --------------------------
  `IndexName`        extends `string`
  `FirstFieldPath`   extends `string`
  `RestFieldPaths`   extends `FieldPaths`\[\]

#### Parameters​

  Name       Type                                           Description
  ---------- ---------------------------------------------- -----------------------------------------------------------------
  `name`     `IndexName`                                    The name of the index.
  `fields`   \[`FirstFieldPath`, \...RestFieldPaths\[\]\]   The fields to index, in order. Must specify at least one field.

#### Returns​

`TableDefinition`\<`Document`, `FieldPaths`, `Expand`\<`Indexes` &
`Record`\<`IndexName`, \[`FirstFieldPath`, \...RestFieldPaths\[\],
`"_creationTime"`\]\>\>, `SearchIndexes`\>

A TableDefinition with this index included.

------------------------------------------------------------------------

### searchIndex​

▸ **searchIndex**\<`IndexName`, `SearchField`, `FilterFields`\>(`name`,
`indexConfig`): `TableDefinition`\<`Document`, `FieldPaths`, `Indexes`,
`Expand`\<`SearchIndexes` & `Record`\<`IndexName`, { `searchField`:
`SearchField` ; `filterFields`: `FilterFields` }\>\>\>

Define a search index on this table.

To learn about search indexes, see Search.

#### Type parameters​

  Name             Type
  ---------------- ----------------------------
  `IndexName`      extends `string`
  `SearchField`    extends `string`
  `FilterFields`   extends `string` = `never`

#### Parameters​

  Name                          Type                 Description
  ----------------------------- -------------------- ---------------------------------------------------------------------------------
  `name`                        `IndexName`          The name of the index.
  `indexConfig`                 `Object`             The search index configuration object.
  `indexConfig.searchField`     `SearchField`        The field to index for full text search. This must be a field of type `string`.
  `indexConfig.filterFields?`   `FilterFields`\[\]   Additional fields to index for fast filtering when running search queries.

#### Returns​

`TableDefinition`\<`Document`, `FieldPaths`, `Indexes`,
`Expand`\<`SearchIndexes` & `Record`\<`IndexName`, { `searchField`:
`SearchField` ; `filterFields`: `FilterFields` }\>\>\>

A TableDefinition with this search index included.

</div>

</div>

</div>

</div>

</div>
