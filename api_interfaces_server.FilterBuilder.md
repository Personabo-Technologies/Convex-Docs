<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   FilterBuilder

<div>

On this page

</div>

<div>

<div>

# Interface: FilterBuilder\<TableInfo\>

</div>

server.FilterBuilder

An interface for defining filters in queries.

`FilterBuilder` has various methods that produce Expressions. These
expressions can be nested together along with constants to express a
filter predicate.

`FilterBuilder` is used within filter to create query filters.

Here are the available methods:

  --------------------- -----------------------------------------------
  **Comparisons**       Error when `l` and `r` are not the same type.
  `eq(l, r)`            `l === r`
  `neq(l, r)`           `l !== r`
  `lt(l, r)`            `l < r`
  `lte(l, r)`           `l <= r`
  `gt(l, r)`            `l > r`
  `gte(l, r)`           `l >= r`
                        
  **Arithmetic**        Error when `l` and `r` are not the same type.
  `add(l, r)`           `l + r`
  `sub(l, r)`           `l - r`
  `mul(l, r)`           `l * r`
  `div(l, r)`           `l / r`
  `mod(l, r)`           `l % r`
  `neg(x)`              `-x`
                        
  **Logic**             Error if any param is not a `bool`.
  `not(x)`              `!x`
  `and(a, b, ..., z)`   `a && b && ... && z`
  `or(a, b, ..., z)`    `a || b || ... || z`
                        
  **Other**             
  `field(fieldPath)`    Evaluates to the field at `fieldPath`.
  --------------------- -----------------------------------------------

## Type parameters​

  Name          Type
  ------------- ----------------------------
  `TableInfo`   extends `GenericTableInfo`

## Methods​

### eq​

▸ **eq**\<`T`\>(`l`, `r`): `Expression`\<`boolean`\>

`l === r`

#### Type parameters​

  Name   Type
  ------ -----------------
  `T`    extends `Value`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### neq​

▸ **neq**\<`T`\>(`l`, `r`): `Expression`\<`boolean`\>

`l !== r`

#### Type parameters​

  Name   Type
  ------ -----------------
  `T`    extends `Value`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### lt​

▸ **lt**\<`T`\>(`l`, `r`): `Expression`\<`boolean`\>

`l < r`

#### Type parameters​

  Name   Type
  ------ -----------------
  `T`    extends `Value`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### lte​

▸ **lte**\<`T`\>(`l`, `r`): `Expression`\<`boolean`\>

`l <= r`

#### Type parameters​

  Name   Type
  ------ -----------------
  `T`    extends `Value`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### gt​

▸ **gt**\<`T`\>(`l`, `r`): `Expression`\<`boolean`\>

`l > r`

#### Type parameters​

  Name   Type
  ------ -----------------
  `T`    extends `Value`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### gte​

▸ **gte**\<`T`\>(`l`, `r`): `Expression`\<`boolean`\>

`l >= r`

#### Type parameters​

  Name   Type
  ------ -----------------
  `T`    extends `Value`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### add​

▸ **add**\<`T`\>(`l`, `r`): `Expression`\<`T`\>

`l + r`

#### Type parameters​

  Name   Type
  ------ ------------------------
  `T`    extends `NumericValue`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`T`\>

------------------------------------------------------------------------

### sub​

▸ **sub**\<`T`\>(`l`, `r`): `Expression`\<`T`\>

`l - r`

#### Type parameters​

  Name   Type
  ------ ------------------------
  `T`    extends `NumericValue`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`T`\>

------------------------------------------------------------------------

### mul​

▸ **mul**\<`T`\>(`l`, `r`): `Expression`\<`T`\>

`l * r`

#### Type parameters​

  Name   Type
  ------ ------------------------
  `T`    extends `NumericValue`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`T`\>

------------------------------------------------------------------------

### div​

▸ **div**\<`T`\>(`l`, `r`): `Expression`\<`T`\>

`l / r`

#### Type parameters​

  Name   Type
  ------ ------------------------
  `T`    extends `NumericValue`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`T`\>

------------------------------------------------------------------------

### mod​

▸ **mod**\<`T`\>(`l`, `r`): `Expression`\<`T`\>

`l % r`

#### Type parameters​

  Name   Type
  ------ ------------------------
  `T`    extends `NumericValue`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `l`    `ExpressionOrValue`\<`T`\>
  `r`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`T`\>

------------------------------------------------------------------------

### neg​

▸ **neg**\<`T`\>(`x`): `Expression`\<`T`\>

`-x`

#### Type parameters​

  Name   Type
  ------ ------------------------
  `T`    extends `NumericValue`

#### Parameters​

  Name   Type
  ------ ----------------------------
  `x`    `ExpressionOrValue`\<`T`\>

#### Returns​

`Expression`\<`T`\>

------------------------------------------------------------------------

### and​

▸ **and**(`...exprs`): `Expression`\<`boolean`\>

`exprs[0] && exprs[1] && ... && exprs[n]`

#### Parameters​

  Name         Type
  ------------ --------------------------------------
  `...exprs`   `ExpressionOrValue`\<`boolean`\>\[\]

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### or​

▸ **or**(`...exprs`): `Expression`\<`boolean`\>

`exprs[0] || exprs[1] || ... || exprs[n]`

#### Parameters​

  Name         Type
  ------------ --------------------------------------
  `...exprs`   `ExpressionOrValue`\<`boolean`\>\[\]

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### not​

▸ **not**(`x`): `Expression`\<`boolean`\>

`!x`

#### Parameters​

  Name   Type
  ------ ----------------------------------
  `x`    `ExpressionOrValue`\<`boolean`\>

#### Returns​

`Expression`\<`boolean`\>

------------------------------------------------------------------------

### field​

▸ **field**\<`FieldPath`\>(`fieldPath`):
`Expression`\<`FieldTypeFromFieldPath`\<`DocumentByInfo`\<`TableInfo`\>,
`FieldPath`\>\>

Evaluates to the field at the given `fieldPath`.

For example, in filter this can be used to examine the values being
filtered.

#### Example​

On this object:

<div>

<div>

    {
      "user": {
        "isActive": true
      }
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

`field("user.isActive")` evaluates to `true`.

#### Type parameters​

  Name          Type
  ------------- ------------------
  `FieldPath`   extends `string`

#### Parameters​

  Name          Type
  ------------- -------------
  `fieldPath`   `FieldPath`

#### Returns​

`Expression`\<`FieldTypeFromFieldPath`\<`DocumentByInfo`\<`TableInfo`\>,
`FieldPath`\>\>

</div>

</div>

</div>

</div>

</div>
