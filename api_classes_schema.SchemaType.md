<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/schema
-   SchemaType

<div>

On this page

</div>

<div>

<div>

# Class: SchemaType\<TypeScriptType, IsOptional, FieldPaths\>

</div>

schema.SchemaType

A Convex type defined in a schema.

These should be constructed using s.

This class encapsulates:

-   The TypeScript type of this Convex type.
-   Whether this field should be optional if it\'s included in an
    object.
-   The TypeScript type for the set of index field paths that can be
    used to build indexes on this type.
-   The table names referenced in `s.id` usages in this type.

## Type parameters​

  Name               Type
  ------------------ -----------------------------
  `TypeScriptType`   `TypeScriptType`
  `IsOptional`       extends `boolean` = `false`
  `FieldPaths`       extends `string` = `never`

## Properties​

### type​

• `Readonly` **type**: `TypeScriptType`

------------------------------------------------------------------------

### isOptional​

• `Readonly` **isOptional**: `IsOptional`

------------------------------------------------------------------------

### fieldPaths​

• `Readonly` **fieldPaths**: `FieldPaths`

------------------------------------------------------------------------

### optional​

• `Readonly` **optional**: `boolean`

------------------------------------------------------------------------

### jsonSchemaType​

• `Readonly` **jsonSchemaType**: `JsonSchemaType`

------------------------------------------------------------------------

### referencedTableNames​

• `Readonly` **referencedTableNames**: `Set`\<`string`\>

## Constructors​

### constructor​

• **new SchemaType**\<`TypeScriptType`, `IsOptional`,
`FieldPaths`\>(`type`, `optional`, `referencedTableNames?`)

#### Type parameters​

  Name               Type
  ------------------ -----------------------------
  `TypeScriptType`   `TypeScriptType`
  `IsOptional`       extends `boolean` = `false`
  `FieldPaths`       extends `string` = `never`

#### Parameters​

  Name                     Type
  ------------------------ -------------------
  `type`                   `JsonSchemaType`
  `optional`               `boolean`
  `referencedTableNames`   `Set`\<`string`\>

</div>

</div>

</div>

</div>

</div>
