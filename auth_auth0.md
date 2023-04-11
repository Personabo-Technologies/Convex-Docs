<div>

<div>

<div>

<div>

-   Home
-   Authentication
-   Auth0

<div>

On this page

</div>

<div>

<div>

# Convex Auth0

</div>

**Example:** Convex Authentication with Auth0

Auth0 is an authentication platform providing login via passwords,
social identity providers, one-time email or SMS access codes,
multi-factor authentication, and single sign on and basic user
management.

## Get started​

Assuming you have a working React app with Convex (if not follow the
Convex React Quickstart first):

1.  <div>

    <div>

    <div>

    Follow the Auth0 React quickstart

    </div>

    Follow the Auth0 React Quickstart.

    Sign up for a free Auth0 account.

    Configure your application, using
    `http://localhost:3000, http://localhost:5173` for Callback and
    Logout URLs and Allowed Web Origins.

    Come back when you finish the *Install the Auth0 React SDK* step.

    </div>

    <div>

    </div>

    </div>

2.  <div>

    <div>

    <div>

    Configure your Convex project

    </div>

    In your terminal run `npx convex auth add` to configure the identity
    provider used by your Convex backend.

    Paste in the `domain` and `clientId` values shown in *Install the
    Auth0 React SDK* step of the Auth0 quickstart or in your Auth0
    application\'s Settings dashboard.

    </div>

    <div>

    </div>

    </div>

3.  <div>

    <div>

    <div>

    Deploy your changes

    </div>

    Run `npx convex dev` to automatically sync your configuration to
    your backend.

    </div>

    <div>

    <div>

    <div>

        npx convex dev

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

4.  <div>

    <div>

    <div>

    Configure ConvexProviderWithAuth0

    </div>

    Now replace your `ConvexProvider` with an `Auth0Provider` wrapping
    `ConvexProviderWithAuth0`

    Follow the *Configure the Auth0Provider component* step of the Auth0
    quickstart to configure the `Auth0Provider`.

    </div>

    <div>

    <div>

    <div>

    src/index.js

    </div>

    <div>

        import { ConvexProviderWithAuth0 } from "convex/react-auth0";
        import { Auth0Provider } from "@auth0/auth0-react";

        root.render(
          <React.StrictMode>
            <Auth0Provider
              domain="your-domain.us.auth0.com"
              clientId="yourclientid"
              authorizationParams={{
                redirect_uri: window.location.origin
              }}
            >
              <ConvexProviderWithAuth0 client={convex} >
                <App />
              </ConvexProviderWithAuth0>
            </Auth0Provider>
          </StrictMode>
        );

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

## Login and logout flows​

Now that you have everything set up, you can use the `useAuth0()` hook
to create login and logout buttons for your app.

The login button will redirect the user to the Auth0 universal login
page. For details see Add Login to Your Application in the Auth0 React
Quickstart.

<div>

<div>

src/login.js

</div>

<div>

    import { useAuth0 } from "@auth0/auth0-react";

    export default function LoginButton() {
      const { loginWithRedirect } = useAuth0();
      return <button onClick={loginWithRedirect}>Log in</button>;
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

The logout button will redirect the user to the Auth0 logout endpoint.
For details see Add Logout to your Application in the Auth0 React
Quickstart.

<div>

<div>

src/logout.js

</div>

<div>

    import { useAuth0 } from "@auth0/auth0-react";

    export default function LogoutButton() {
      const { logout } = useAuth0();
      return (
        <button
          onClick={() =>
            logout({ logoutParams: { returnTo: window.location.origin } })
          }
        >
          Log out
        </button>
      );
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Logged-in and logged-out views​

Use the `useConvexAuth()` hook instead of the `useAuth0` hook when you
need to check whether the user is logged in or not. The `useConvex` hook
makes sure that the browser has fetched the auth token needed to make
authenticated requests to your Convex backend:

<div>

<div>

src/App.js

</div>

<div>

    import { useConvexAuth } from "convex/react";

    function App() {
      const { isLoading, isAuthenticated } = useConvexAuth();

      return (
        <div className="App">
          {isAuthenticated ? "Logged in" : "Logged out or still loading"}
        </div>
      );
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

You can also use the `Authenticated`, `Unauthenticated` and
`AuthLoading` helper components which use the `useConvexAuth` hook under
the hood:

<div>

<div>

src/App.js

</div>

<div>

    import { Authenticated, Unauthenticated, AuthLoading } from "convex/react";

    function App() {
      return (
        <div className="App">
          <Authenticated>Logged in</Authenticated>
          <Unauthenticated>Logged out</Unauthenticated>
          <AuthLoading>Still loading</AuthLoading>
        </div>
      );
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## User information in React​

You can access information about the authenticated user like their name
from the `useAuth0` hook:

<div>

<div>

src/badge.js

</div>

<div>

    import { useAuth0 } from "@auth0/auth0-react";

    export default function Badge() {
      const { user } = useAuth0();
      return <span>Logged in as {user.name}</span>;
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## User information in functions​

See Auth in Functions to learn about how to access information about the
authenticated user in your queries, mutations and actions.

See Storing Users in the Convex Database to learn about how to store
user information in the Convex database.

## Under the hood​

The authentication flow looks like this under the hood:

1.  The user clicks a login button
2.  The user is redirected to a page where they log in via whatever
    method you configure in Auth0
3.  After a successful login Auth0 redirects back to your page, or a
    different page which you configure via the `authorizationParams`
    prop.
4.  The `Auth0Provider` now knows that the user is authenticated.
5.  The `ConvexProviderWithAuth0` fetches an auth token from Auth0.
6.  After the token is returned all current and future function calls
    will include the auth token in their HTTP headers.
7.  Your Convex backend will read the token from the request headers and
    pass it to Auth0 to check that it is valid and the user is still
    logged in.

`ConvexProviderWithAuth0` ensures that the auth token is refetched when
needed.

</div>

</div>

</div>

</div>

</div>
