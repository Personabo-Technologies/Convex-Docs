<div>

<div>

<div>

<div>

-   Home
-   Functions
-   HTTP Endpoints

<div>

On this page

</div>

<div>

<div>

# HTTP Endpoints

</div>

**Example:** HTTP Endpoints

HTTP endpoints allow you to build an HTTP API right in Convex!

HTTP endpoints take in a Request and return a Response following the
Fetch API. HTTP endpoints can manipulate the request and response
directly, and interact with data in Convex indirectly by running
queries, mutations, and actions. HTTP endpoints might be used for
receiving webhooks from external applications or defining a public HTTP
API.

HTTP endpoints are exposed at
`https://<your deployment name>.convex.site` (e.g.
`https://happy-animal-123.convex.site`).

## Defining HTTP Endpoints​

HTTP endpoint handlers are defined using the `httpEndpoint` wrapper.
This function has an `HttpEndpointCtx` as its first argument, which
provides `auth` and `storage`, as well as `runQuery`, `runMutation`,
`runAction`. The second argument is the `Request` that was made.

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)tip

</div>

<div>

Consider using `runQuery`, `runMutation`, and `runAction` with Internal
Functions to prevent users from calling these functions directly.

</div>

</div>

Here\'s an example:

<div>

<div>

convex/http.js

</div>

<div>

    import { httpEndpoint } from "./_generated/server";

    const postMessage = httpEndpoint(async ({ runMutation }, request) => {
      const { author, body } = await request.json();

      await runMutation("sendMessage", {
        body: `Sent via HTTP endpoint: ${body}`,
        author,
      });
      return new Response(null, {
        status: 200,
      });
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

`httpRouter` in the `convex/http.js` / `convex/http.ts` file links the
handlers to routes:

<div>

<div>

convex/http.js

</div>

<div>

    const http = httpRouter();

    http.route({
      path: "/postMessage",
      method: "POST",
      handler: postMessage,
    });

    // Define additional routes
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

You can now call this endpoint via HTTP and interact with data stored in
the Convex Database. HTTP endpoints are exposed on
`https://<your deployment name>.convex.site`.

<div>

<div>

    export DEPLOYMENT_NAME=... # example: "happy-animal-123"
    curl -d '{ "author": "User 123", "body": "Hello world" }' \
        -H 'content-type: application/json' "https://$DEPLOYMENT_NAME.convex.site/postMessage"

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Like other Convex functions, you can view your HTTP endpoints in the
Functions view of your dashboard and view logs produced by them in the
Logs view.

## Limits​

HTTP endpoints run in the same environment as queries and mutations so
also do not have access to Node.js-specific JavaScript APIs. HTTP
endpoints can call actions, which do run in Node.js.

Like actions, HTTP endpoints may have side-effects and will not be
automatically retried by Convex when errors occur. It is a
responsibility of the caller to handle errors and retry the request if
appropriate.

Request and response size is limited to 20MB.

HTTP endpoints support request and response body types of `.text()`,
`.json()`, and `.arrayBuffer()`.

Note that you don\'t need to define an HTTP endpoint to call your
queries, mutations and actions over HTTP if you control the caller,
since you can use use the JavaScript `ConvexHttpClient` or the Python
client to call these functions directly.

## Common patterns​

### File Storage​

HTTP endpoints can be used to handle uploading and fetching stored
files, see File Storage with HTTP endpoints.

### CORS​

To make requests to HTTP endpoints from a website you need to add
Cross-Origin Resource Sharing (CORS) headers to your HTTP endpoints.

There are existing resources for exactly which CORS headers are required
based on the use case. This site provides an interactive walkthrough for
what CORS headers to add. Here\'s an example of adding CORS headers to a
Convex HTTP endpoint:

<div>

<div>

convex/http.js

</div>

<div>

    http.route({
      path: "/sendImage",
      method: "POST",
      handler: httpEndpoint(async ({ storage, runMutation }, request) => {
        // Store the image
        const storageId = await storage.store(request);
        const author = new URL(request.url).searchParams.get("author");

        // Save the storage ID to the messages table via a mutation
        await runMutation("sendMessage:sendImage", { storageId, author });
        return new Response(null, {
          status: 200,
          // CORS headers
          headers: new Headers({
            // e.g. https://mywebsite.com
            "Access-Control-Allow-Origin": process.env.CLIENT_ORIGIN,
            Vary: "origin",
          }),
        });
      }),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Here\'s an example of handling a pre-flight `OPTIONS` request:

<div>

<div>

convex/http.js

</div>

<div>

    // Pre-flight request for /sendImage
    http.route({
      path: "/sendImage",
      method: "OPTIONS",
      handler: httpEndpoint(async ({}, request) => {
        // Make sure the necessary headers are present
        // for this to be a valid pre-flight request
        let headers = request.headers;
        if (
          headers.get("Origin") !== null &&
          headers.get("Access-Control-Request-Method") !== null &&
          headers.get("Access-Control-Request-Headers") !== null
        ) {
          return new Response(null, {
            headers: new Headers({
              // e.g. https://mywebsite.com
              "Access-Control-Allow-Origin": process.env.CLIENT_ORIGIN,
              "Access-Control-Allow-Methods": "POST",
              "Access-Control-Allow-Headers": "Content-Type, Digest",
              "Access-Control-Max-Age": "86400",
            }),
          });
        } else {
          return new Response();
        }
      }),
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>
