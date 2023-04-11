<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/schema

<div>

On this page

</div>

<div>

<div>

# Module: schema

</div>

Utilities for defining the schema of your Convex project.

## Usage​

Schemas should be placed in a `schema.ts` file in your `convex/`
directory.

Schema definitions should be built using defineSchema, defineTable, and
s. Make sure to export the schema as the default export.

<div>

<div>

    import { defineSchema, defineTable, s } from "convex/schema";

     export default defineSchema({
       messages: defineTable({
         body: s.string(),
         user: s.id("users"),
       }),
       users: defineTable({
         name: s.string(),
       }),
     });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

To learn more about schemas, see Defining a Schema.

## Classes​

-   SchemaType
-   TableDefinition
-   SchemaDefinition

## Interfaces​

-   SearchIndexConfig
-   DefineSchemaOptions

## Variables​

### s​

• `Const` **s**: `Object`

The schema builder.

This builder allows you to define the types of documents stored in
Convex.

#### Type declaration​

  Name         Type
  ------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------
  `id`         \<TableName\>(`tableName`: `TableName`) =\> `SchemaType`\<`GenericId`\<`TableName`\>, `false`, `never`\>
  `null`       () =\> `SchemaType`\<`null`, `false`, `never`\>
  `number`     () =\> `SchemaType`\<`number`, `false`, `never`\>
  `bigint`     () =\> `SchemaType`\<`bigint`, `false`, `never`\>
  `boolean`    () =\> `SchemaType`\<`boolean`, `false`, `never`\>
  `string`     () =\> `SchemaType`\<`string`, `false`, `never`\>
  `bytes`      () =\> `SchemaType`\<`ArrayBuffer`, `false`, `never`\>
  `literal`    \<T\>(`literal`: `T`) =\> `SchemaType`\<`T`, `false`, `never`\>
  `array`      \<T\>(`values`: `SchemaType`\<`T`, `false`, `any`\>) =\> `SchemaType`\<`T`\[\], `false`, `never`\>
  `set`        \<T\>(`values`: `SchemaType`\<`T`, `false`, `any`\>) =\> `SchemaType`\<`Set`\<`T`\>, `false`, `never`\>
  `map`        \<K, V\>(`keys`: `SchemaType`\<`K`, `false`, `any`\>, `values`: `SchemaType`\<`V`, `false`, `any`\>) =\> `SchemaType`\<`Map`\<`K`, `V`\>, `false`, `never`\>
  `object`     \<T\>(`schema`: `T`) =\> `ObjectSchemaType`\<`T`\>
  `union`      \<T\>(\...`schemaTypes`: `T`) =\> `SchemaType`\<`T`\[`number`\]\[`"type"`\], `false`, `T`\[`number`\]\[`"fieldPaths"`\]\>
  `any`        () =\> `SchemaType`\<`any`, `false`, `string`\>
  `optional`   \<T\>(`inner`: `T`) =\> `SchemaType`\<`T`\[`"type"`\], `true`, `T`\[`"fieldPaths"`\]\>

## Functions​

### defineTable​

▸ **defineTable**\<`DocumentSchema`\>(`documentSchema`):
`TableDefinition`\<`ExtractDocument`\<`DocumentSchema`\>,
`ExtractFieldPaths`\<`DocumentSchema`\>\>

Define a table in a schema.

You can either specify the schema of your documents as an object like

<div>

<div>

    defineTable({
      field: s.string()
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

or as a schema type like

<div>

<div>

    defineTable(
     s.union(
       s.object({...}),
       s.object({...})
     )
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Type parameters​

  Name               Type
  ------------------ ---------------------------------------------------------------------------------------
  `DocumentSchema`   extends `SchemaType`\<`Record`\<`string`, `any`\>, `false`, `any`, `DocumentSchema`\>

#### Parameters​

  Name               Type               Description
  ------------------ ------------------ ---------------------------------------------
  `documentSchema`   `DocumentSchema`   The type of documents stored in this table.

#### Returns​

`TableDefinition`\<`ExtractDocument`\<`DocumentSchema`\>,
`ExtractFieldPaths`\<`DocumentSchema`\>\>

A TableDefinition for the table.

▸ **defineTable**\<`DocumentSchema`\>(`documentSchema`):
`TableDefinition`\<`ExtractDocument`\<`ObjectSchemaType`\<`DocumentSchema`\>\>,
`ExtractFieldPaths`\<`ObjectSchemaType`\<`DocumentSchema`\>\>\>

Define a table in a schema.

You can either specify the schema of your documents as an object like

<div>

<div>

    defineTable({
      field: s.string()
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

or as a schema type like

<div>

<div>

    defineTable(
     s.union(
       s.object({...}),
       s.object({...})
     )
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Type parameters​

  Name               Type
  ------------------ -------------------------------------------------------------------
  `DocumentSchema`   extends `Record`\<`string`, `SchemaType`\<`any`, `any`, `any`\>\>

#### Parameters​

  Name               Type               Description
  ------------------ ------------------ ---------------------------------------------
  `documentSchema`   `DocumentSchema`   The type of documents stored in this table.

#### Returns​

`TableDefinition`\<`ExtractDocument`\<`ObjectSchemaType`\<`DocumentSchema`\>\>,
`ExtractFieldPaths`\<`ObjectSchemaType`\<`DocumentSchema`\>\>\>

A TableDefinition for the table.

------------------------------------------------------------------------

### defineSchema​

▸ **defineSchema**\<`Schema`, `IsStrict`\>(`schema`, `options?`):
`SchemaDefinition`\<`Schema`, `IsStrict`\>

Define the schema of this Convex project.

This should be exported from a `schema.ts` file in your `convex/`
directory like:

<div>

<div>

    export default defineSchema({
      ...
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Type parameters​

  Name         Type
  ------------ ----------------------------
  `Schema`     extends `GenericSchema`
  `IsStrict`   extends `boolean` = `true`

#### Parameters​

  Name         Type                                  Description
  ------------ ------------------------------------- ---------------------------------------------------------------------------------
  `schema`     `Schema`                              A map from table name to TableDefinition for all of the tables in this project.
  `options?`   `DefineSchemaOptions`\<`IsStrict`\>   Optional configuration. See DefineSchemaOptions for a full description.

#### Returns​

`SchemaDefinition`\<`Schema`, `IsStrict`\>

The schema.

## Type Aliases​

### GenericSchema​

Ƭ **GenericSchema**: `Record`\<`string`, `TableDefinition`\>

A type describing the schema of a Convex project.

This should be constructed using defineSchema, defineTable, and s.

------------------------------------------------------------------------

### DataModelFromSchemaDefinition​

Ƭ **DataModelFromSchemaDefinition**\<`SchemaDef`\>:
`MaybeMakeLooseDataModel`\<{ \[TableName in keyof
SchemaDef\[\"tables\"\] & string\]: SchemaDef\[\"tables\"\]\[TableName\]
extends TableDefinition\<infer Document, infer FieldPaths, infer
Indexes, infer SearchIndexes\> ? MaybeMakeLooseTableInfo\<Object,
SchemaDef\[\"isStrict\"\]\> : never }, `SchemaDef`\[`"isStrict"`\]\>

Internal type used in Convex code generation!

Convert a SchemaDefinition into a GenericDataModel.

#### Type parameters​

  Name          Type
  ------------- ------------------------------------------------
  `SchemaDef`   extends `SchemaDefinition`\<`any`, `boolean`\>

------------------------------------------------------------------------

### Infer​

Ƭ **Infer**\<`SType`\>: `SType`\[`"type"`\]

Extract a TypeScript type from a piece of a schema definition.

Example usage:

<div>

<div>

    const objectSchema = s.object({
      property: s.string(),
    });
    type MyObject = Infer<typeof objectSchema>; // { property: string }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Type parameters​

  Name      Type                                          Description
  --------- --------------------------------------------- ----------------------------------------------
  `SType`   extends `SchemaType`\<`any`, `any`, `any`\>   The type of a SchemaType constructed with s.

</div>

</div>

</div>

</div>

</div>
