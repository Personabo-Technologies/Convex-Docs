<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   IndexRangeBuilder

<div>

On this page

</div>

<div>

<div>

# Interface: IndexRangeBuilder\<Document, IndexFields, FieldNum\>

</div>

server.IndexRangeBuilder

Builder to define an index range to query.

An index range is a description of which documents Convex should
consider when running the query.

An index range is always a chained list of:

1.  0 or more equality expressions defined with `.eq`.
2.  \[Optionally\] A lower bound expression defined with `.gt` or
    `.gte`.
3.  \[Optionally\] An upper bound expression defined with `.lt` or
    `.lte`.

**You must step through fields in index order.**

Each equality expression must compare a different index field, starting
from the beginning and in order. The upper and lower bounds must follow
the equality expressions and compare the next field.

For example, if there is an index of messages on
`["projectId", "priority"]`, a range searching for \"messages in
\'myProjectId\' with priority at least 100\" would look like:

<div>

<div>

    q.eq("projectId", myProjectId)
     .gte("priority", 100)

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

**The performance of your query is based on the specificity of the
range.**

This class is designed to only allow you to specify ranges that Convex
can efficiently use your index to find. For all other filtering use
filter.

To learn about indexes, see Indexes.

## Type parameters​

  Name            Type
  --------------- ------------------------------
  `Document`      extends `GenericDocument`
  `IndexFields`   extends `GenericIndexFields`
  `FieldNum`      extends `number` = `0`

## Hierarchy​

-   `LowerBoundIndexRangeBuilder`\<`Document`,
    `IndexFields`\[`FieldNum`\]\>

    ↳ **`IndexRangeBuilder`**

## Methods​

### eq​

▸ **eq**(`fieldName`, `value`): `NextIndexRangeBuilder`\<`Document`,
`IndexFields`, `FieldNum`\>

Restrict this range to documents where `doc[fieldName] === value`.

#### Parameters​

  Name          Type                                                                  Description
  ------------- --------------------------------------------------------------------- ------------------------------------------------------------------------
  `fieldName`   `IndexFields`\[`FieldNum`\]                                           The name of the field to compare. Must be the next field in the index.
  `value`       `FieldTypeFromFieldPath`\<`Document`, `IndexFields`\[`FieldNum`\]\>   The value to compare against.

#### Returns​

`NextIndexRangeBuilder`\<`Document`, `IndexFields`, `FieldNum`\>

------------------------------------------------------------------------

### gt​

▸ **gt**(`fieldName`, `value`):
`UpperBoundIndexRangeBuilder`\<`Document`, `IndexFields`\[`FieldNum`\]\>

Restrict this range to documents where `doc[fieldName] > value`.

#### Parameters​

  Name          Type                                                                  Description
  ------------- --------------------------------------------------------------------- ------------------------------------------------------------------------
  `fieldName`   `IndexFields`\[`FieldNum`\]                                           The name of the field to compare. Must be the next field in the index.
  `value`       `FieldTypeFromFieldPath`\<`Document`, `IndexFields`\[`FieldNum`\]\>   The value to compare against.

#### Returns​

`UpperBoundIndexRangeBuilder`\<`Document`, `IndexFields`\[`FieldNum`\]\>

#### Inherited from​

LowerBoundIndexRangeBuilder.gt

------------------------------------------------------------------------

### gte​

▸ **gte**(`fieldName`, `value`):
`UpperBoundIndexRangeBuilder`\<`Document`, `IndexFields`\[`FieldNum`\]\>

Restrict this range to documents where `doc[fieldName] >= value`.

#### Parameters​

  Name          Type                                                                  Description
  ------------- --------------------------------------------------------------------- ------------------------------------------------------------------------
  `fieldName`   `IndexFields`\[`FieldNum`\]                                           The name of the field to compare. Must be the next field in the index.
  `value`       `FieldTypeFromFieldPath`\<`Document`, `IndexFields`\[`FieldNum`\]\>   The value to compare against.

#### Returns​

`UpperBoundIndexRangeBuilder`\<`Document`, `IndexFields`\[`FieldNum`\]\>

#### Inherited from​

LowerBoundIndexRangeBuilder.gte

------------------------------------------------------------------------

### lt​

▸ **lt**(`fieldName`, `value`): `IndexRange`

Restrict this range to documents where `doc[fieldName] < value`.

#### Parameters​

  Name          Type                                                                  Description
  ------------- --------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------
  `fieldName`   `IndexFields`\[`FieldNum`\]                                           The name of the field to compare. Must be the same index field used in the lower bound (`.gt` or `.gte`) or the next field if no lower bound was specified.
  `value`       `FieldTypeFromFieldPath`\<`Document`, `IndexFields`\[`FieldNum`\]\>   The value to compare against.

#### Returns​

`IndexRange`

#### Inherited from​

LowerBoundIndexRangeBuilder.lt

------------------------------------------------------------------------

### lte​

▸ **lte**(`fieldName`, `value`): `IndexRange`

Restrict this range to documents where `doc[fieldName] <= value`.

#### Parameters​

  Name          Type                                                                  Description
  ------------- --------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------
  `fieldName`   `IndexFields`\[`FieldNum`\]                                           The name of the field to compare. Must be the same index field used in the lower bound (`.gt` or `.gte`) or the next field if no lower bound was specified.
  `value`       `FieldTypeFromFieldPath`\<`Document`, `IndexFields`\[`FieldNum`\]\>   The value to compare against.

#### Returns​

`IndexRange`

#### Inherited from​

LowerBoundIndexRangeBuilder.lte

</div>

</div>

</div>

</div>

</div>
