<div>

<div>

<div>

<div>

-   Home
-   Authentication
-   Custom

<div>

On this page

</div>

<div>

<div>

# Custom Auth Integration

</div>

Convex can be integrated with any identity provider supporting the
OpenID Connect protocol. At minimum this means that the provider can
issue ID tokens and verify them. The ID token is passed from the client
to your Convex backend which ensures that the token is valid and enables
you to query the user information embedded in the token, as described in
Auth in Functions.

## Integrating a new identity provider​

The `ConvexProviderWithAuth` component provides a convenient abstraction
for building an auth integration similar to the ones Convex provides for
Clerk and Auth0.

In the following example we build an integration with an imaginary
\"ProviderX\", whose React integration includes
`AuthProviderXReactProvider` and `useProviderXAuth` hook.

First we replace `ConvexProvider` with `AuthProviderXReactProvider`
wrapping `ConvexProviderWithAuth` at the root of our app:

<div>

<div>

src/index.js

</div>

<div>

    import { AuthProviderXReactProvider } from "providerX";
    import { ConvexProviderWithAuth } from "convex/react";

    root.render(
      <React.StrictMode>
        <AuthProviderXReactProvider>
          <ConvexProviderWithAuth client={convex} useAuth={useAuthFromProviderX}>
            <App />
          </ConvexProviderWithAuth>
        </AuthProviderXReactProvider>
      </StrictMode>
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

All we really need is to implement the `useAuthFromProviderX` hook which
gets passed to the `ConvexProviderWithAuth` component.

This `useAuthFromProviderX` hook provides a translation between the auth
provider API and the `ConvexReactClient` API, which is ultimately
responsible for making sure that the ID token is passed down to your
Convex backend.

<div>

<div>

src/ConvexProviderWithProviderX.js

</div>

<div>

    function useAuthFromProviderX() {
      const { isLoading, isAuthenticated, getToken } = useProviderXAuth();
      const fetchAccessToken = useCallback(
        async () => {
          // Here you can do whatever transformation to get the ID Token
          // or null
          return await getToken();
        },
        // If `getToken` isn't correctly memoized
        // remove it from this dependency array
        [getToken]
      );
      return useMemo(
        () => ({
          // Whether the auth provider is in a loading state
          isLoading: isLoading,
          // Whether the auth provider has the user signed in
          isAuthenticated: isAuthenticated ?? false,
          // The async function to fetch the ID token
          fetchAccessToken,
        }),
        [isLoading, isAuthenticated, fetchAccessToken]
      );
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Using the new provider​

If you successfully follow the steps above you can now use the standard
Convex utilities for checking the authentication state: the
`useConvexAuth()` hook and the `Authenticated`, `Unauthenticated` and
`AuthLoading` helper components.

See Logged-in and logged-out views for examples of using these.

</div>

</div>

</div>

</div>

</div>
