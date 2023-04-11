<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Generated Code
-   dataModel.js

<div>

On this page

</div>

<div>

<div>

# dataModel.js

</div>

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)This code
is generated

</div>

<div>

These exports are not directly available in the `convex` package!

Instead you must run `npx convex codegen` to create
`convex/_generated/dataModel.js` and `convex/_generated/dataModel.d.ts`.

</div>

</div>

Generated data model types.

## Types​

### TableNames​

Ƭ **TableNames**: `string`

The names of all of your Convex tables.

------------------------------------------------------------------------

### Doc​

Ƭ **Doc**`<TableName>`: `Object`

The type of a document stored in Convex.

#### Type parameters​

  Name          Type                   Description
  ------------- ---------------------- -----------------------------------------------------------
  `TableName`   extends `TableNames`   A string literal type of the table name (like \"users\").

------------------------------------------------------------------------

### DataModel​

Ƭ **DataModel**: `Object`

A type describing your Convex data model.

This type includes information about what tables you have, the type of
documents stored in those tables, and the indexes defined on them.

This type is used to parameterize methods like `queryGeneric` and
`mutationGeneric` to make them type-safe.

## Classes​

### Id​

An identifier for a document in Convex.

Convex documents are uniquely identified by their `Id`, which is
accessible on the `_id` field. To learn more, see Data Modeling.

Documents can be loaded using `db.get(id)` in query and mutation
functions.

**Important**: Use `myId.equals(otherId)` to check for equality. Using
`===` will not work because two different instances of `Id` can refer to
the same document.

`Id`s are 17 bytes long and consist of:

-   A 15-byte random value.
-   A 2-byte timestamp representing the document\'s creation, in days
    since the Unix epoch.

This is encoded in base 62 (\[0-9A-Za-z\]).

This is an alias of `GenericId` that is typed for your data model.

#### Type parameters​

  Name          Type                   Description
  ------------- ---------------------- -----------------------------------------------------------
  `TableName`   extends `TableNames`   A string literal type of the table name (like \"users\").

------------------------------------------------------------------------

#### Properties​

##### tableName​

• `Readonly` **tableName**: `TableName`

The table name this `Id` references.

------------------------------------------------------------------------

##### id​

• `Readonly` **id**: `string`

The identifier string.

This contains the characters `[0-9A-Za-z]`.

#### Constructors​

##### constructor​

• `**new Id**<TableName>`(`tableName`, `id`)

##### Type parameters​

  Name          Type
  ------------- ------------------
  `TableName`   extends `string`

##### Parameters​

  Name          Type
  ------------- -------------
  `tableName`   `TableName`
  `id`          `string`

#### Methods​

##### equals​

▸ **equals**(`other`): `boolean`

Check if this `Id` refers to the same document as another `Id`.

###### Parameters​

  Name      Type              Description
  --------- ----------------- -------------------------------
  `other`   `Id<TableName>`   The other `Id` to compare to.

###### Returns​

`boolean`

`true` if the objects refer to the same document.

------------------------------------------------------------------------

##### fromJSON​

▸ `Static` **fromJSON**(`obj`): `Id` `<string>`

Parse an `Id` from its JSON representation.

------------------------------------------------------------------------

##### toJSON​

▸ **toJSON**(): `JSONValue`

Convert an `Id` into its JSON representation.

###### Returns​

`JSONValue`

------------------------------------------------------------------------

##### toString​

▸ **toString**(): `string`

Convert an `Id` into its string representation.

This includes the identifier but not the table name.

###### Returns​

`string`

##### inspect​

▸ **inspect**(): `string`

Pretty-print this `Id` for debugging.

###### Returns​

`string`

</div>

</div>

</div>

</div>

</div>
