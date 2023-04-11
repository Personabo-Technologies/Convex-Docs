<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   ActionCtx

<div>

On this page

</div>

<div>

<div>

# Interface: ActionCtx\<API\>

</div>

server.ActionCtx

A set of services for use within Convex action.

The context is passed as the first argument to any Convex action run on
the server.

If you\'re using code generation, use the `ActionCtx` type in
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

## Properties​

### scheduler​

• **scheduler**: `Scheduler`\<`API`\>

------------------------------------------------------------------------

### auth​

• **auth**: `Auth`

</div>

</div>

</div>

</div>

</div>
