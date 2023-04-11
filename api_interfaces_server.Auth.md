<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   Auth

<div>

On this page

</div>

<div>

<div>

# Interface: Auth

</div>

server.Auth

An interface to access information about the currently authenticated
user within Convex query and mutation functions.

## Methods​

### getUserIdentity​

▸ **getUserIdentity**(): `Promise`\<`null` \| `UserIdentity`\>

Get details about the currently authenticated user.

#### Returns​

`Promise`\<`null` \| `UserIdentity`\>

A promise that resolves to a UserIdentity if the Convex client was
configured with a valid ID token and `null` otherwise.

</div>

</div>

</div>

</div>

</div>
