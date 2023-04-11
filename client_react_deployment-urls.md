<div>

<div>

<div>

<div>

-   Home
-   Client Libraries
-   React
-   Deployment URLs

<div>

On this page

</div>

<div>

<div>

# Configuring Deployment URL

</div>

When connecting to your backend it\'s important to correctly configure
the deployment URL.

### Create a Convex project​

The first time you run

<div>

<div>

    npx convex dev

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

in your project directory you will be asked about creating a new Convex
project.

Your new project includes two deployments: *production* and
*development*, each located at a URL displayed after the project is
created. You will be asked about saving these URLs to `.env` and
`.env.local` file respectively.

You can find the URLs of all deployments in a project by visiting the
settings section of each deployment on your Convex dashboard.

### Configure the client​

Construct a Convex React client by passing in the URL of the Convex
deployment. There should generally be a single Convex client in a
frontend application.

<div>

<div>

src/index.js

</div>

<div>

    import { ConvexProvider, ConvexReactClient } from "convex/react";
    const deploymentURL = process.env.REACT_APP_CONVEX_URL;
    const convex = new ConvexReactClient(deploymentURL);

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

While this URL can be hardcoded, it\'s convenient to use an environment
variable to determine which deployment the client should connect to.

Use an environment variable name accessible from your client code
according to the frontend framework or bundler you\'re using.

### Choosing environment variable names​

To avoid unintentionally exposing secret environment variables in
frontend code, many bundlers require environment variables referenced in
frontend code to use a specific prefix.

Create React App requires environment variables used in frontend code to
begin with `REACT_APP_`, so the code above uses `REACT_APP_CONVEX_URL`.

Vite requires environment variables used in frontend code start with
`VITE_`, so `VITE_CONVEX_URL` is a good name.

Next.js requires them to begin with `NEXT_PUBLIC_`, so
`NEXT_PUBLIC_CONVEX_URL` is a good name.

Bundlers provide different ways to access these variables too: while
Vite uses `import.meta.env.VARIABLE_NAME`, many other tools like Next.js
use the Node.js-like `process.env.VARIABLE_NAME`

<div>

<div>

    import { ConvexProvider, ConvexReactClient } from "convex/react";

    const convex = new ConvexReactClient(process.env.NEXT_PUBLIC_CONVEX_URL);

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

`.env` files are a common way to wire up different environment variable
values in development and production environments. `npx convex dev` will
offer to save the deployment URLs to the corresponding `.env` file,
while trying to infer which bundler your project uses.

<div>

<div>

.env

</div>

<div>

    NEXT_PUBLIC_CONVEX_URL=https://guiltless-dog-960.convex.cloud

    # examples of other environment variables that might be passed to the frontend
    NEXT_PUBLIC_SENTRY_DSN=https://123abc@o123.ingest.sentry.io/1234
    NEXT_PUBLIC_LAUNCHDARKLY_SDK_CLIENT_SIDE_ID=01234567890abcdef

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
