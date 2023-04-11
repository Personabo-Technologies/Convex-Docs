<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/browser
-   ClientOptions

<div>

On this page

</div>

<div>

<div>

# Interface: ClientOptions

</div>

browser.ClientOptions

Options for InternalConvexClient.

## Properties​

### unsavedChangesWarning​

• `Optional` **unsavedChangesWarning**: `boolean`

Whether to prompt the user if they have unsaved changes pending when
navigating away or closing a web page.

This is only possible when the `window` object exists, i.e. in a
browser.

The default value is `true` in browsers.

------------------------------------------------------------------------

### webSocketConstructor​

• `Optional` **webSocketConstructor**: `Object`

#### Call signature​

• **new ClientOptions**(`url`, `protocols?`): `WebSocket`

Specifies an alternate WebSocket constructor to use for client
communication with the Convex cloud. The default behavior is to use
`WebSocket` from the global environment.

##### Parameters​

  Name           Type
  -------------- --------------------------
  `url`          `string` \| `URL`
  `protocols?`   `string` \| `string`\[\]

##### Returns​

`WebSocket`

#### Type declaration​

  Name           Type
  -------------- -------------
  `prototype`    `WebSocket`
  `CLOSED`       `number`
  `CLOSING`      `number`
  `CONNECTING`   `number`
  `OPEN`         `number`

------------------------------------------------------------------------

### verbose​

• `Optional` **verbose**: `boolean`

Adds additional logging for debugging purposes.

The default value is `false`.

</div>

</div>

</div>

</div>

</div>
