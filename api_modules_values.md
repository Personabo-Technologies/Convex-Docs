<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/values

<div>

On this page

</div>

<div>

<div>

# Module: values

</div>

Utilities for working with values stored in Convex.

You can see the full set of supported types at Types.

## Classes​

-   GenericId

## Type Aliases​

### JSONValue​

Ƭ **JSONValue**: `null` \| `boolean` \| `number` \| `string` \|
`JSONValue`\[\] \| { `[key: string]`: `JSONValue`; }

The type of JavaScript values serializable to JSON.

------------------------------------------------------------------------

### GenericIdConstructor​

Ƭ **GenericIdConstructor**\<`TableNames`\>: `Object`

#### Type parameters​

  Name           Type
  -------------- ------------------
  `TableNames`   extends `string`

#### Call signature​

• **new GenericIdConstructor**\<`TableName`\>(`tableName`, `id`):
`GenericId`\<`TableName`\>

Internal type used in Convex code generation.

##### Type parameters​

  Name          Type
  ------------- ------------------
  `TableName`   extends `string`

##### Parameters​

  Name          Type
  ------------- -------------
  `tableName`   `TableName`
  `id`          `string`

##### Returns​

`GenericId`\<`TableName`\>

#### Type declaration​

  Name          Type
  ------------- --------------------------------------------
  `prototype`   `GenericId`\<`string`\>
  `fromJSON`    (`obj`: `any`) =\> `GenericId`\<`string`\>

------------------------------------------------------------------------

### Value​

Ƭ **Value**: `GenericId`\<`string`\> \| `null` \| `bigint` \| `number`
\| `boolean` \| `string` \| `ArrayBuffer` \| `Value`\[\] \|
`Set`\<`Value`\> \| `Map`\<`Value`, `Value`\> \| { `[key: string]`:
`undefined` \| `Value`; }

A value supported by Convex.

Values can be:

-   stored inside of documents.
-   used as arguments and return types to queries and mutation
    functions.

You can see the full set of supported types at Types.

------------------------------------------------------------------------

### NumericValue​

Ƭ **NumericValue**: `bigint` \| `number`

The types of Value that can be used to represent numbers.

## Functions​

### jsonToConvex​

▸ **jsonToConvex**(`value`): `Value`

Parse a Convex value from its JSON representation.

This function will revive classes like GenericId that have been
serialized to JSON, parse out `BigInt`s, and so on.

To learn more about Convex values, see Types.

#### Parameters​

  Name      Type          Description
  --------- ------------- ---------------------------------------------------------------------------------
  `value`   `JSONValue`   The JSON representation of a Convex value previously created with convexToJson.

#### Returns​

`Value`

The JavaScript representation of the Convex value.

------------------------------------------------------------------------

### convexToJson​

▸ **convexToJson**(`value`): `JSONValue`

Convert a Convex value to its JSON representation.

Use jsonToConvex to recreate the original value.

To learn more about Convex values, see Types.

#### Parameters​

  Name      Type      Description
  --------- --------- --------------------------------------
  `value`   `Value`   A Convex value to convert into JSON.

#### Returns​

`JSONValue`

The JSON representation of `value`.

</div>

</div>

</div>

</div>

</div>
