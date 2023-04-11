<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   HttpRouter

<div>

On this page

</div>

<div>

<div>

# Class: HttpRouter

</div>

server.HttpRouter

HTTP router for specifying the paths and methods of httpEndpointGenerics

An example `convex/http.js` file might look like this.

<div>

<div>

    import { httpRouter } from "./_generated/server";
    import { getMessagesByAuthor } from "./getMessagesByAuthor";
    import { httpEndpoint } from "./_generated/server";

    const http = httpRouter();

    // HTTP endpoints can be defined inline...
    http.route({
      path: "/message",
      method: "POST",
      handler: httpEndpoint(async ({ runMutation }, request) => {
        const { author, body } = await request.json();

        await runMutation("sendMessage", { body, author });
        return new Response(null, {
          status: 200,
        });
      })
    });

    // ...or they can be imported from other files.
    http.route({
      path: "/getMessagesByAuthor",
      method: "GET",
      handler: getMessagesByAuthor,
    });

    // Convex expects the router to be the default export of `convex/http.js`.
    export default http;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Constructors​

### constructor​

• **new HttpRouter**()

## Properties​

### exactRoutes​

• **exactRoutes**: `Map`\<`string`, `Map`\<`"POST"` \| `"GET"` \|
`"PUT"` \| `"DELETE"` \| `"OPTIONS"` \| `"PATCH"`,
`PublicHttpEndpoint`\>\>

------------------------------------------------------------------------

### prefixRoutes​

• **prefixRoutes**: `Map`\<`"POST"` \| `"GET"` \| `"PUT"` \| `"DELETE"`
\| `"OPTIONS"` \| `"PATCH"`, `Map`\<`string`, `PublicHttpEndpoint`\>\>

------------------------------------------------------------------------

### isRouter​

• **isRouter**: `boolean` = `true`

## Methods​

### route​

▸ **route**(`spec`): `void`

Specify an HttpEndpoint to be used to respond to requests for an HTTP
method (e.g. \"GET\") and a path or pathPrefix.

Paths must begin with a slash. Path prefixes must also end in a slash.

<div>

<div>

    // matches `/profile` (but not `/profile/`)
    http.route({ path: "/profile", method: "GET", handler: getProfile})

    // matches `/profiles/`, `/profiles/abc`, and `/profiles/a/c/b` (but not `/profile`)
    http.route({ pathPrefix: "/profile/", method: "GET", handler: getProfile})

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Parameters​

  Name     Type
  -------- -------------
  `spec`   `RouteSpec`

#### Returns​

`void`

------------------------------------------------------------------------

### getRoutes​

▸ **getRoutes**(): readonly \[`string`, `"POST"` \| `"GET"` \| `"PUT"`
\| `"DELETE"` \| `"OPTIONS"` \| `"PATCH"`, (\...`args`: `any`\[\]) =\>
`any`\]\[\]

Returns a list of routed HTTP endpoints.

These are used to populate the list of routes shown in the Functions
page of the Convex dashboard.

#### Returns​

readonly \[`string`, `"POST"` \| `"GET"` \| `"PUT"` \| `"DELETE"` \|
`"OPTIONS"` \| `"PATCH"`, (\...`args`: `any`\[\]) =\> `any`\]\[\]

-   an array of \[path, method, endpoint\] tuples.

------------------------------------------------------------------------

### lookup​

▸ **lookup**(`path`, `method`): `null` \| readonly
\[`PublicHttpEndpoint`, `"POST"` \| `"GET"` \| `"PUT"` \| `"DELETE"` \|
`"OPTIONS"` \| `"PATCH"`, `string`\]

Returns the appropriate HTTP endpoint and its routed request path and
method.

The path and method returned are used for logging and metrics, and
should match up with one of the routes returned by `getRoutes`.

For example,

<div>

<div>

    http.route({ pathPrefix: "/profile/", method: "GET", handler: getProfile});

    http.lookup("/profile/abc", "GET") // returns [getProfile, "GET", "/profile/*"]

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

#### Parameters​

  Name       Type
  ---------- --------------------------------------------------------------------------------------
  `path`     `string`
  `method`   `"POST"` \| `"GET"` \| `"PUT"` \| `"DELETE"` \| `"OPTIONS"` \| `"PATCH"` \| `"HEAD"`

#### Returns​

`null` \| readonly \[`PublicHttpEndpoint`, `"POST"` \| `"GET"` \|
`"PUT"` \| `"DELETE"` \| `"OPTIONS"` \| `"PATCH"`, `string`\]

-   a tuple \[PublicHttpEndpoint, method, path\] or null.

------------------------------------------------------------------------

### runRequest​

▸ **runRequest**(`argsStr`): `Promise`\<`string`\>

Given a JSON string representation of a Request object, return a
Response by routing the request and running the appropriate endpoint or
returning a 404 Response.

#### Parameters​

  Name        Type       Description
  ----------- ---------- ----------------------------------------------
  `argsStr`   `string`   a JSON string representing a Request object.

#### Returns​

`Promise`\<`string`\>

-   a Response object.

</div>

</div>

</div>

</div>

</div>
