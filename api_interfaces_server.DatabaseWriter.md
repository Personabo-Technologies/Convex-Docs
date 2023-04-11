<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   DatabaseWriter

<div>

On this page

</div>

<div>

<div>

# Interface: DatabaseWriter\<DataModel\>

</div>

server.DatabaseWriter

An interface to read from and write to the database within Convex
mutation functions.

Convex guarantees that all writes within a single mutation are executed
atomically, so you never have to worry about partial writes leaving your
data in an inconsistent state. See the Convex Guide for the guarantees
Convex provides your functions.

If you\'re using code generation, use the `DatabaseReader` type in
`convex/_generated/server.d.ts` which is typed for your data model.

## Type parameters​

  Name          Type
  ------------- ----------------------------
  `DataModel`   extends `GenericDataModel`

## Hierarchy​

-   `DatabaseReader`\<`DataModel`\>

    ↳ **`DatabaseWriter`**

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

#### Inherited from​

DatabaseReader.get

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

#### Inherited from​

DatabaseReader.query

------------------------------------------------------------------------

### insert​

▸ **insert**\<`TableName`\>(`table`, `value`):
`Promise`\<`GenericId`\<`TableName`\>\>

Insert a new document into a table.

#### Type parameters​

  Name          Type
  ------------- ------------------
  `TableName`   extends `string`

#### Parameters​

  Name      Type                                                                                                     Description
  --------- -------------------------------------------------------------------------------------------------------- ------------------------------------------------------
  `table`   `TableName`                                                                                              The name of the table to insert a new document into.
  `value`   `Expand`\<`BetterOmit`\<`DocumentByName`\<`DataModel`, `TableName`\>, `"_creationTime"` \| `"_id"`\>\>   The Value to insert into the given table.

#### Returns​

`Promise`\<`GenericId`\<`TableName`\>\>

-   GenericId of the new document.

------------------------------------------------------------------------

### patch​

▸ **patch**\<`TableName`\>(`id`, `value`): `Promise`\<`void`\>

Patch an existing document, merging its value with a new values.

Any overlapping fields in the two documents will be overwritten with
their new value.

#### Type parameters​

  Name          Type
  ------------- ------------------
  `TableName`   extends `string`

#### Parameters​

  Name      Type                                                        Description
  --------- ----------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `id`      `GenericId`\<`TableName`\>                                  The GenericId of the document to patch.
  `value`   `Partial`\<`DocumentByName`\<`DataModel`, `TableName`\>\>   The partial GenericDocument to merge into the specified document. If this new value specifies system fields like `_id`, they must match the document\'s existing field values.

#### Returns​

`Promise`\<`void`\>

------------------------------------------------------------------------

### replace​

▸ **replace**\<`TableName`\>(`id`, `value`): `Promise`\<`void`\>

Replace the value of an existing document, overwriting its old value.

#### Type parameters​

  Name          Type
  ------------- ------------------
  `TableName`   extends `string`

#### Parameters​

  Name      Type                                                                                                                                                                                                                     Description
  --------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------
  `id`      `GenericId`\<`TableName`\>                                                                                                                                                                                               The GenericId of the document to replace.
  `value`   `Expand`\<`Expand`\<`BetterOmit`\<`DocumentByName`\<`DataModel`, `TableName`\>, `"_creationTime"` \| `"_id"`\>\> & `Partial`\<`Pick`\<`DocumentByName`\<`DataModel`, `TableName`\>, `"_creationTime"` \| `"_id"`\>\>\>   The new GenericDocument for the document. This value can omit the system fields, and the database will fill them in.

#### Returns​

`Promise`\<`void`\>

------------------------------------------------------------------------

### delete​

▸ **delete**(`id`): `Promise`\<`void`\>

Delete an existing document.

#### Parameters​

  Name   Type                                                    Description
  ------ ------------------------------------------------------- ------------------------------------------
  `id`   `GenericId`\<`TableNamesInDataModel`\<`DataModel`\>\>   The GenericId of the document to remove.

#### Returns​

`Promise`\<`void`\>

</div>

</div>

</div>

</div>

</div>
