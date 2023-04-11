<div>

<div>

<div>

<div>

-   Home
-   Client Libraries
-   React
-   Next.js

<div>

On this page

</div>

<div>

<div>

# Next.js

</div>

Next.js is a React web development framework. When used with Convex,
Next.js provides:

-   File-system based routing
-   API routes
-   Fast refresh in development
-   Font and image optimization

and more!

## Getting started​

You can create a new Next.js app with

<div>

<div>

    npx create-next-app myapp --use-npm --typescript

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Then install the Convex client library and initialize a new project.

<div>

<div>

    cd myapp
    npm install convex
    npx convex login
    npx convex init

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Adding the Convex provider​

Next.js routes are defined in the `pages/` directory, each file defining
the component that runs only on that page. The component in
`pages/_app.jsx` acts as a parent for all pages, persisting through
client-side page navigations. This makes `pages/_app.jsx` an excellent
place to add the `<ConvexProvider/>` wrapper when Convex is used
throughout a Next.js app.

<div>

<div>

pages/\_app.jsx

</div>

<div>

    import { ConvexProvider, ConvexReactClient } from "convex/react";

    const convex = new ConvexReactClient(process.env.NEXT_PUBLIC_CONVEX_URL);

    function MyApp({ Component, pageProps }) {
      return (
        <ConvexProvider client={convex}>
          <Component {...pageProps} />;
        </ConvexProvider>
      );
    }

    export default MyApp;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Adding client-side authentication​

The simplest approach to authentication in Next.js is to keep it
client-side.

Auth0 describes this approach in Next.js Authentication with Auth0
guide, describing it in \"Next.js Static Site Approach\" and
\"Serverless with the user on the frontend.\"

To require login on every page of your application you can add logic to
`_app.jsx` to conditionally render page content, blocking it until the
user is logged in.

If you\'re using Auth0, the helper component `ConvexProviderWithAuth0`
can be imported from `convex/react-auth0` after installing the Auth0
React library with `npm install @auth0/auth0-react`.

<div>

<div>

pages/\_app.jsx

</div>

<div>

    import { ConvexReactClient } from "convex/react";
    import { ConvexProviderWithAuth0 } from "convex/react-auth0";
    import { Auth0Provider } from "@auth0/auth0-react";

    const convex = new ConvexReactClient(process.env.NEXT_PUBLIC_CONVEX_URL);

    export default function MyApp({ Component, pageProps }) {
      return (
        <Auth0Provider
          domain={process.env.NEXT_AUTH0_DOMAIN}
          clientId={process.env.NEXT_AUTH0_CLIENT_ID}
          authorizationParams={{
            redirect_uri:
              typeof window === "undefined" ? undefined : window.location.origin,
          }}
        >
          <ConvexProviderWithAuth0 client={convex}>
            <Component {...pageProps} />
          </ConvexProviderWithAuth0>
        </Auth0Provider>
      );
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Custom loading and logged out views can be built with the helper
`Authenticated`, `Unauthenticated` and `AuthLoading` components from
`convex/react`, see the Convex Next.js demo for an example.

If only some routes of your app require login, the same helpers can be
used directly in page components that do require login instead of being
shared between all pages from `pages/_app.jsx`. Share a single
ConvexReactClient instance between pages to avoid needing to reconnect
to Convex on client-side page navigation.

Read more about authenticating users with Convex in Authentication. In
particular, be sure to run `npx convex auth add` to configure Convex for
your chosen auth provider.

## API routes​

Next.js supports building API routes by adding files to the `pages/api`
directory.

To load and edit Convex data in your endpoints, you can use the
ConvexHttpClient to call your query and mutation functions:

<div>

<div>

pages/api/clicks.js

</div>

<div>

    import { ConvexHttpClient } from "convex/browser";

    const convex = new ConvexHttpClient(process.env.NEXT_PUBLIC_CONVEX_URL);

    export default async function handler(req, res) {
      const clicks = await convex.query("getCounter")({ counterName: "clicks" });
      res.status(200).json({ clicks });
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Server-side rendering​

**We currently recommend client-side rendering Convex data when using
Next.js.** This is because data from Convex is fully reactive. Convex
needs a connection from your deployment to the browser in order to push
updates as data changes and that must happen on the client.

If you need Convex data on the server, you can load data from Convex in
`getStaticProps` or `getServerSideProps`, but it will be non-reactive.
To do this, use the ConvexHttpClient to call query functions just like
you would in API routes.

To make authenticated requests to Convex during server-side rendering,
the ConvexHttpClient instance needs authentication info present
server-side. Auth0 describes this approach in Serverless with the user
on the backend. When server-side rendering, call
`ConvexHttpClient.setAuth` to fetch the user\'s identity token before
making the query.

We are investigating ways to combine Next.js server-side rendering with
end-to-end reactivity. Stay tuned!

</div>

</div>

</div>

</div>

</div>
