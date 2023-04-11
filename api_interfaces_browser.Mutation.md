<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/browser
-   Mutation

<div>

On this page

</div>

<div>

<div>

# Interface: Mutation\<F\>

</div>

browser.Mutation

## Type parameters​

  Name   Type
  ------ --------------------------------------------------------
  `F`    extends (\...`args`: `any`\[\]) =\> `Promise`\<`any`\>

## Callable​

### Mutation​

▸ **Mutation**(`...args`): `Promise`\<`Awaited`\<`ReturnType`\<`F`\>\>\>

Execute the mutation on the server, returning a `Promise` of its return
value.

#### Parameters​

  Name        Type                  Description
  ----------- --------------------- -----------------------------
  `...args`   `Parameters`\<`F`\>   Arguments for the mutation.

#### Returns​

`Promise`\<`Awaited`\<`ReturnType`\<`F`\>\>\>

The return value of the server-side function call.

</div>

</div>

</div>

</div>

</div>
