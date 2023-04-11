<div>

<div>

<div>

<div>

-   Home
-   Authentication
-   Clerk

<div>

On this page

</div>

<div>

<div>

# Convex Clerk

</div>

Clerk is an authentication platform providing login via passwords,
social identity providers, one-time email or SMS access codes, and
multi-factor authentication and basic user management.

## Get started​

Assuming you have a working React app with Convex (if not follow the
Convex React Quickstart first):

1.  <div>

    <div>

    <div>

    Sign up for Clerk

    </div>

    Sign up for a free Clerk account at clerk.com/sign-up.

    </div>

    <div>

    </div>

    </div>

2.  <div>

    <div>

    <div>

    Create an application in Clerk

    </div>

    Choose how you want your users to sign in.

    </div>

    <div>

    </div>

    </div>

3.  <div>

    <div>

    <div>

    Create a JWT Template

    </div>

    In the JWT Templates section of the Clerk dashboard tap on *+ New
    template* and choose **Convex**

    </div>

    <div>

    </div>

    </div>

4.  <div>

    <div>

    <div>

    Customize Claims and copy Issuer URL

    </div>

    Customize the *Claims* with the following template.

    Copy the *Issuer* URL from the Issuer input field and hit Apply
    Changes.

    </div>

    <div>

    <div>

    <div>

    Claims

    </div>

    <div>

        {
          "aud": "convex",
          "email": "{{user.primary_email_address}}",
          "picture": "{{user.profile_image_url}}",
          "given_name": "{{user.first_name}}",
          "updated_at": "{{user.updated_at}}",
          "family_name": "{{user.last_name}}",
          "email_verified": "{{user.email_verified}}"
        }

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

5.  <div>

    <div>

    <div>

    Configure your Convex project

    </div>

    In your terminal run `npx convex auth add` to configure the identity
    provider used by your Convex backend.

    Paste in the *Issuer* URL and `convex` (the value of the \"aud\"
    field from the JWT template).

    </div>

    <div>

    </div>

    </div>

6.  <div>

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

7.  <div>

    <div>

    <div>

    Install clerk

    </div>

    In a new terminal window, install the Clerk React library

    </div>

    <div>

    <div>

    <div>

        npm install @clerk/clerk-react

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

8.  <div>

    <div>

    <div>

    Get your Clerk Publishable key

    </div>

    On the Clerk dashboard in the API Keys section copy the Publishable
    key

    </div>

    <div>

    </div>

    </div>

9.  <div>

    <div>

    <div>

    Configure ConvexProviderWithClerk

    </div>

    Now replace your `ConvexProvider` with `ClerkProvider` wrapping
    `ConvexProviderWithClerk`.

    Paste in the Publishable key to the `publishableKey` prop of
    `ClerkProvider`.

    </div>

    <div>

    <div>

    <div>

    src/index.js

    </div>

    <div>

        import { ClerkProvider } from "@clerk/clerk-clerk";
        import { ConvexProviderWithClerk } from "convex/react-clerk";

        root.render(
          <React.StrictMode>
            <ClerkProvider publishableKey="pk_test_....">
              <ConvexProviderWithClerk client={convex}>
                <App />
              </ConvexProviderWithClerk>
            </ClerkProvider>
          </StrictMode>
        );

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

## Login and logout Flows​

Now that you have everything set up, you can use the `SignInButton`
component to create a login flow for your app.

The login button will open the Clerk configured login dialog:

<div>

<div>

src/App.js

</div>

<div>

    import { SignInButton } from "@clerk/clerk-react";

    function App() {
      return (
        <div className="App">
          <SignInButton mode="modal" />
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

To enable a logout flow you can use the `SignOutButton` from
`@clerk/clerk-react` or the `UserButton` which opens a dialog that
includes a sign out button.

## Logged-in and logged-out views​

Use the `useConvexAuth()` hook instead of Clerk\'s `useAuth` hook when
you need to check whether the user is logged in or not. The
`useConvexAuth` hook makes sure that the browser has fetched the auth
token needed to make authenticated requests to your Convex backend:

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
`AuthLoading` helper components instead of the similarly named Clerk
components. These components use the `useConvex` hook under the hood:

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
from Clerk\'s `useUser` hook. See the User doc for the list of available
fields:

<div>

<div>

src/badge.js

</div>

<div>

    import { useUser } from "@clerk/clerk-react";

    export default function Badge() {
      const { user } = useUser();
      return <span>Logged in as {user.fullName}</span>;
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

## Next.js, React Native Expo, Gatsby​

The `ConvexProviderWithClerk` component supports all Clerk integrations
based on the `@clerk/clerk-react` library. Simply replace the package
from which you import the `ClerkProvider` component and follow any
additional steps in Clerk docs.

## Under the hood​

The authentication flow looks like this under the hood:

1.  The user clicks a login button
2.  The user is redirected to a page where they log in via whatever
    method you configure in Clerk
3.  After a successful login Clerk redirects back to your page, or a
    different page which you configure via the `afterSignIn` prop.
4.  The `ClerkProvider` now knows that the user is authenticated.
5.  The `ConvexProviderWithClerk` fetches an auth token from Clerk.
6.  After the token is returned all current and future function calls
    will include the auth token in their HTTP headers.
7.  Your Convex backend will read the token from the request headers and
    pass it to Clerk to check that it is valid and the user is still
    logged in.

`ConvexProviderWithClerk` ensures that the auth token is refetched when
needed.

</div>

</div>

</div>

</div>

</div>
