<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/browser
-   Query

<div>

On this page

</div>

<div>

<div>

# Interface: Query\<F\>

</div>

browser.Query

## Type parameters​

  Name   Type
  ------ --------------------------------------------------------
  `F`    extends (\...`args`: `any`\[\]) =\> `Promise`\<`any`\>

## Callable​

### Query​

▸ **Query**(`...args`): `Promise`\<`Awaited`\<`ReturnType`\<`F`\>\>\>

Execute the query on the server, returning a `Promise` of the return
value.

#### Parameters​

  Name        Type                  Description
  ----------- --------------------- --------------------------
  `...args`   `Parameters`\<`F`\>   Arguments for the query.

#### Returns​

`Promise`\<`Awaited`\<`ReturnType`\<`F`\>\>\>

The result of the query.

</div>

</div>

</div>

</div>

</div>
