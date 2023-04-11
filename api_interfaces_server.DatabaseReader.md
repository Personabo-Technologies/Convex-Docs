<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   DatabaseReader

<div>

On this page

</div>

<div>

<div>

# Interface: DatabaseReader\<DataModel\>

</div>

server.DatabaseReader

An interface to read from the database within Convex query functions.

The two entry points are get, which fetches a single document by its
GenericId, or query, which starts building a query.

If you\'re using code generation, use the `DatabaseReader` type in
`convex/_generated/server.d.ts` which is typed for your data model.

## Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`

## Hierarchy​

-   **`DatabaseReader`**

    ↳ `DatabaseWriter`

## Methods​

### get​

▸ **get**\<`TableName`\>(`id`): `Promise`\<`null` \|
`DocumentByName`\<`DataModel`, `TableName`\>\>

Fetch a single document from the database by its GenericId.

#### Type parameters​

  Name          Type
  ------------- ------------------
  `TableName`   extends `string`

#### Parameters​

  Name   Type                         Description
  ------ ---------------------------- -----------------------------------------------------------
  `id`   `GenericId`\<`TableName`\>   The GenericId of the document to fetch from the database.

#### Returns​

`Promise`\<`null` \| `DocumentByName`\<`DataModel`, `TableName`\>\>

-   The GenericDocument of the document at the given GenericId, or
    `null` if it no longer exists.

------------------------------------------------------------------------

### query​

▸ **query**\<`TableName`\>(`tableName`):
`QueryInitializer`\<`NamedTableInfo`\<`DataModel`, `TableName`\>\>

Begin a query for the given table name.

Queries don\'t execute immediately, so calling this method and extending
its query are free until the results are actually used.

#### Type parameters​

  Name          Type
  ------------- ------------------
  `TableName`   extends `string`

#### Parameters​

  Name          Type          Description
  ------------- ------------- ---------------------------------
  `tableName`   `TableName`   The name of the table to query.

#### Returns​

`QueryInitializer`\<`NamedTableInfo`\<`DataModel`, `TableName`\>\>

-   A QueryInitializer object to start building a query.

</div>

</div>

</div>

</div>

</div>
