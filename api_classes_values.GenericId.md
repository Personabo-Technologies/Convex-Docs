<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/values
-   GenericId

<div>

On this page

</div>

<div>

<div>

# Class: GenericId\<TableName\>

</div>

values.GenericId

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
    since the Unix epoch. This is encoded in base 62 (\[0-9A-Za-z\]).

If you\'re using code generation, use the `Id` class typed for your data
model in `convex/_generated/dataModel.js`.

## Type parameters​

  Name          Type               Description
  ------------- ------------------ -----------------------------------------------------------
  `TableName`   extends `string`   A string literal type of the table name (like \"users\").

## Properties​

### tableName​

• `Readonly` **tableName**: `TableName`

The table name this GenericId references.

------------------------------------------------------------------------

### id​

• `Readonly` **id**: `string`

The identifier string.

This contains the characters `[0-9A-Za-z]`.

## Constructors​

### constructor​

• **new GenericId**\<`TableName`\>(`tableName`, `id`)

#### Type parameters​

  Name          Type
  ------------- ------------------
  `TableName`   extends `string`

#### Parameters​

  Name          Type
  ------------- -------------
  `tableName`   `TableName`
  `id`          `string`

## Methods​

### equals​

▸ **equals**(`other`): `boolean`

Check if this GenericId refers to the same document as another
GenericId.

#### Parameters​

  Name      Type        Description
  --------- ----------- ------------------------------------
  `other`   `unknown`   The other GenericId to compare to.

#### Returns​

`boolean`

`true` if the objects refer to the same document.

------------------------------------------------------------------------

### fromJSON​

▸ `Static` **fromJSON**(`obj`): `GenericId`\<`string`\>

Parse a GenericId from its JSON representation.

#### Parameters​

  Name    Type
  ------- -------
  `obj`   `any`

#### Returns​

`GenericId`\<`string`\>

------------------------------------------------------------------------

### toJSON​

▸ **toJSON**(): `JSONValue`

Convert a GenericId into its JSON representation.

#### Returns​

`JSONValue`

------------------------------------------------------------------------

### toString​

▸ **toString**(): `string`

Convert a GenericId into its string representation.

This includes the identifier but not the table name.

#### Returns​

`string`

------------------------------------------------------------------------

### inspect​

▸ **inspect**(): `string`

Pretty-print this GenericId for debugging.

#### Returns​

`string`

</div>

</div>

</div>

</div>

</div>
