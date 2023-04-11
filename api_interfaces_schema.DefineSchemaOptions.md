<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/schema
-   DefineSchemaOptions

<div>

On this page

</div>

<div>

<div>

# Interface: DefineSchemaOptions\<IsStrict\>

</div>

schema.DefineSchemaOptions

Options for defineSchema.

## Type parameters​

  Name         Type
  ------------ -------------------
  `IsStrict`   extends `boolean`

## Properties​

### strict​

• `Optional` **strict**: `IsStrict`

Whether to strictly enforce this schema.

If this schema is not strictly enforced, its type will permit:

1.  Using additional tables not explicitly listed in the schema.
2.  Using additional properties not explicitly listed in the tables.

Loose schemas are useful for rapid prototyping.

By default the schema is considered strict.

------------------------------------------------------------------------

### exportDocumentType​

• `Optional` **exportDocumentType**: `boolean`

</div>

</div>

</div>

</div>

</div>
