<div>

<div>

<div>

<div>

-   Home
-   Production
-   Hosting and Deployment
-   Environment Variables

<div>

On this page

</div>

<div>

<div>

# Environment Variables

</div>

Environment variables are key-value pairs that are useful for storing
values you wouldn\'t want to put in code or in a table, such as an API
key. You can store environment variables in Convex through the
dashboard, and you can access them in functions using `process.env`.

## Storing environment variables​

Under Deployment Settings in the Dashboard, you can see a list of
environment variables in your deployment.

You can add up to 10 environment variables. Environment variable names
cannot be more than 40 characters long, and they must start with a
letter and only contain letters numbers, and underscores. Environment
variable values cannot be larger than 8KB.

You can modify environment variables using the \"Edit\" button:

## Accessing environment variables​

You can access environment variables in Convex functions using
`process.env.KEY`. You can only access environment variables that are
stored in your deployment (see instructions above). An environment
variable can be a `string` or `undefined` in Typescript. Here is an
example of accessing an environment variable with the key `GIPHY_KEY`:

<div>

<div>

    function giphyUrl(query) {
      return (
        "https://api.giphy.com/v1/gifs/translate?api_key=" +
        process.env.GIPHY_KEY +
        "&s=" +
        encodeURIComponent(query)
      );
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Using environment variables in dev and prod deployments​

Since environment variables are stored per-deployment, you can use
different values for the same key in dev and prod deployments. This can
be useful for when you have different external accounts you\'d like to
use depending on the environment. For example, you might have a dev and
prod SendGrid account for sending emails, and your function expects an
environment variable called `SENDGRID_API_KEY` that should work in both
environments. If you expect an environment variable to be present in a
function, you will have to add it to **all** deployments that function
is deployed to. In this example, you would add an environment variable
with the name `SENDGRID_API_KEY` to your dev and prod deployments, with
a different value for dev than for prod.

## System environment variables​

The following environment variables are always available in Convex
functions:

-   `CONVEX_CLOUD_URL` - Your deployment URL (eg.
    `https://dusty-nightingale-847.convex.cloud`) for use with Convex
    clients.
-   `CONVEX_SITE_URL` - Your deployment site URL (eg.
    `https://dusty-nightingale-847.convex.site`) for use with HTTP
    Endpoints

</div>

</div>

</div>

</div>

</div>
