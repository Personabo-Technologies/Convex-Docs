<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   HttpEndpointCtx

<div>

On this page

</div>

<div>

<div>

# Interface: HttpEndpointCtx\<API\>

</div>

server.HttpEndpointCtx

A set of services for use within Convex HTTP endpoint.

The context is passed as the first argument to any Convex HTTP endpoint
run on the server.

If you\'re using code generation, use the `HttpEndpointCtx` type in
`convex/_generated/server.d.ts` which is typed for your data model.

## Type parameters​

  Name    Type
  ------- ----------------------
  `API`   extends `GenericAPI`

## Methods​

### runQuery​

▸ **runQuery**\<`Name`\>(`name`, `...args`):
`Promise`\<`ReturnType`\<`NamedQuery`\<`API`, `Name`\>\>\>

Runs the Convex query with the given name and arguments.

Consider using an internalQuery to prevent users from calling the query
directly.

#### Type parameters​

  Name     Type
  -------- ------------------
  `Name`   extends `string`

#### Parameters​

  Name        Type
  ----------- -----------------------------------------------
  `name`      `Name`
  `...args`   `Parameters`\<`NamedQuery`\<`API`, `Name`\>\>

#### Returns​

`Promise`\<`ReturnType`\<`NamedQuery`\<`API`, `Name`\>\>\>

------------------------------------------------------------------------

### runMutation​

▸ **runMutation**\<`Name`\>(`name`, `...args`):
`Promise`\<`ReturnType`\<`NamedMutation`\<`API`, `Name`\>\>\>

Runs the Convex mutation with the given name and arguments.

Consider using an internalMutation to prevent users from calling the
mutation directly.

#### Type parameters​

  Name     Type
  -------- ------------------
  `Name`   extends `string`

#### Parameters​

  Name        Type
  ----------- --------------------------------------------------
  `name`      `Name`
  `...args`   `Parameters`\<`NamedMutation`\<`API`, `Name`\>\>

#### Returns​

`Promise`\<`ReturnType`\<`NamedMutation`\<`API`, `Name`\>\>\>

------------------------------------------------------------------------

### runAction​

▸ **runAction**\<`Name`\>(`name`, `...args`):
`Promise`\<`ReturnType`\<`NamedAction`\<`API`, `Name`\>\>\>

Runs the Convex action with the given name and arguments.

Consider using an internalAction to prevent users from calling the
action directly.

#### Type parameters​

  Name     Type
  -------- ------------------
  `Name`   extends `string`

#### Parameters​

  Name        Type
  ----------- ------------------------------------------------
  `name`      `Name`
  `...args`   `Parameters`\<`NamedAction`\<`API`, `Name`\>\>

#### Returns​

`Promise`\<`ReturnType`\<`NamedAction`\<`API`, `Name`\>\>\>

## Properties​

### auth​

• **auth**: `Auth`

------------------------------------------------------------------------

### storage​

• **storage**: `StorageHttpWriter`

</div>

</div>

</div>

</div>

</div>
