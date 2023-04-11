<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/react
-   ReactAction

<div>

On this page

</div>

<div>

<div>

# Interface: ReactAction\<API, Name\>

</div>

react.ReactAction

## Type parameters​

  Name     Type
  -------- --------------------------------------
  `API`    extends `GenericAPI`
  `Name`   extends `PublicActionNames`\<`API`\>

## Callable​

### ReactAction​

▸ **ReactAction**(`...args`):
`Promise`\<`ReturnType`\<`NamedAction`\<`API`, `Name`\>\>\>

Execute the function on the server, returning a `Promise` of its return
value.

#### Parameters​

  Name        Type                                             Description
  ----------- ------------------------------------------------ ------------------------------------------------------
  `...args`   `Parameters`\<`NamedAction`\<`API`, `Name`\>\>   Arguments for the function to pass up to the server.

#### Returns​

`Promise`\<`ReturnType`\<`NamedAction`\<`API`, `Name`\>\>\>

The return value of the server-side function call.

</div>

</div>

</div>

</div>

</div>
