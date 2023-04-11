<div>

<div>

<div>

<div>

-   Home
-   Database
-   Defining a Schema

<div>

On this page

</div>

<div>

<div>

# Defining a Schema

</div>

**Example:** TypeScript and Schema

A schema is a description of

1.  the tables in your Convex project
2.  the type of documents within your tables

While it is possible to use Convex *without* defining a schema, adding a
`schema.ts` file will give you additional type safety throughout your
app.

We recommend beginning your project without a schema for rapid
prototyping and then adding a schema once you\'ve solidified your plan.
To learn more see our Schema Philosophy.

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)Schema
Enforcement

</div>

<div>

Currently schemas are a \"types only\" feature. Adding a schema will
give you precise, code generated types, but won\'t change the runtime
behavior of your application.

In the future Convex will support enforcing your schema and rejecting
documents that don\'t match it.

</div>

</div>

## Writing schemas​

Schemas are defined in a `schema.ts` file in your `convex/` directory
and look like:

<div>

<div>

convex/schema.ts

</div>

<div>

    import { defineSchema, defineTable, s } from "convex/schema";

    export default defineSchema({
      messages: defineTable({
        body: s.string(),
        user: s.id("users"),
      }),
      users: defineTable({
        name: s.string(),
        tokenIdentifier: s.string(),
      }).index("by_token", ["tokenIdentifier"]),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This schema (which is based on our users and auth example), has 3
tables: channels, messages, and users. Each table is defined using the
`defineTable` function. Within each table, the document type is defined
using our schema builder, `s`. In addition to the fields listed, Convex
will also automatically add `_id` and `_creationTime` fields. To learn
more, see System Fields.

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)Generating
a Schema

</div>

<div>

While writing your schema, it can be helpful to consult the Convex
Dashboard. The \"Generate Schema\" button in the \"Data\" view suggests
a schema declaration based on the data in your tables.

</div>

</div>

### Supported types​

The schema builder supports all of the Convex types. It also supports
union types, literal types, any types, and optional types.

#### Unions​

You can describe fields that could be one of multiple types using
`s.union`:

<div>

<div>

    defineTable({
      stringOrNumber: s.union(s.string(), s.number()),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

If your table stores multiple different types of documents, you can also
use `s.union` at the top level:

<div>

<div>

    defineTable(
      s.union(
        s.object({
          string: s.string(),
        }),
        s.object({
          number: s.number(),
        })
      )
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Literals​

Fields that are a constant can be expressed with `s.literal`:

<div>

<div>

    defineTable({
      oneTwoOrThree: s.union(
        s.literal("one"),
        s.literal("two"),
        s.literal("three")
      ),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Any​

Fields that could take on any value can be represented with `s.any()`:

<div>

<div>

    defineTable({
      anyValue: s.any(),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This corresponds to the `any` type in TypeScript.

#### Optional fields​

You can describe optional fields by wrapping their type with
`s.optional(...)`:

<div>

<div>

    defineTable({
      optionalString: s.optional(s.string()),
      optionalNumber: s.optional(s.number()),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This corresponds to marking fields as optional with `?` in TypeScript.

### Schema strictness​

By default schemas are considered strict. This means that the TypeScript
type produced the schema will only support tables and properties
explicitly listed in your schema.

Sometimes it\'s useful to only define part of your schema. For example,
if you are rapidly prototyping, it could be useful to try out a new
table before adding it your `schema.ts` file.

You can disable strict mode by passing `strict: false` in the
`DefineSchemaOptions` object:

<div>

<div>

    defineSchema(
      {
        // Define tables here.
      },
      {
        strict: false,
      }
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

When strict mode is disabled, the schema will permit:

1.  Using additional tables not explicitly listed in the schema.
2.  Using additional properties not explicitly listed in the tables.

## Using schemas​

Once you\'ve defined a schema, `npx convex dev` will produce new
versions of `dataModel.d.ts` and `server.d.ts`.

### `Doc<TableName>`​

The `Doc` type from `dataModel.d.ts` provides document types for all of
your tables. You can use these both when writing Convex functions and in
your React components:

<div>

<div>

MessageView.tsx

</div>

<div>

    import { Doc } from "../convex/_generated/dataModel";

    function MessageView(props: { message: Doc<"messages"> }) {
      ...
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### `query` and `mutation`​

The `query` and `mutation` functions in `server.js` have the same API as
before but now provide a `db` with more precise types. Functions like
`db.insert(table, document)` now understand your schema. Additionally
database queries will now return the correct document type (not `any`).

### `Infer<typeof schemaValue>`​

The `Infer` type allows you to turn pieces of your schema into
TypeScript types. This can be useful to remove duplication between your
schema and TypeScript types:

<div>

<div>

convex/schema.ts

</div>

<div>

    import { defineSchema, defineTable, Infer, s } from "convex/schema";

    const nestedObject = s.object({
      property: s.string(),
    });

    // Resolves to `{property: string}`.
    export type NestedObject = Infer<typeof nestedObject>;

    export default defineSchema({
      tableName: defineTable({
        nested: nestedObject,
      }),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>
