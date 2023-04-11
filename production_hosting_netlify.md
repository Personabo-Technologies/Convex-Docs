<div>

<div>

<div>

<div>

-   Home
-   Production
-   Hosting and Deployment
-   Netlify

<div>

On this page

</div>

<div>

<div>

# Using Convex with Netlify

</div>

**New to Convex?** Convex is the reactive backend-as-a-service for web
developers. Convex allows you to define your backend with JavaScript
functions that push updates your React components in realtime. To get
started, head to the tutorial or the homepage.

Hosting your Convex app on Netlify allows you to automatically re-deploy
both your backend and your frontend whenever you push to git.

## Deploying to Netlify​

If you haven\'t done so, create a Netlify account. This is free for
small projects and should take less than a minute to set up. When asked
to deploy a first project just click the link to skip that step for now.

Once you have a working project that runs locally and have created a
GitHub repo for it, create a project at https://app.netlify.com/start
and link the project to the source code repository.

We need to make two changes from the Netlify defaults.

First, **override the \"Build Command\" to be
`npm run build && npx convex deploy`**. We\'ll discuss why this is
necessary in a bit.

Second, let\'s **add a Convex deploy key as an environment variable**:

1.  Go to the Convex Dashboard.
2.  Find your project and click \"Settings\".
3.  Copy the \"Deploy key\".
4.  In Netlify, click \"Advanced\" \> \"New Variable\".
5.  Create an environment variable with the key `CONVEX_DEPLOY_KEY` and
    paste the deploy key as the value.

If your Convex project is nested under a subdirectory you\'ll also need
to change \"Base directory\" accordingly.

Click the **Deploy Site** button and your work here is done!

Netlify will automatically publish your site to a URL
`https://<site-name>.netlify.app` listed at the top of the site overview
page. Every time you push a git revision, Netlify will automatically
deploy your Convex functions and publish your site changes.

## How it works​

In Netlify, we overrode the \"Build Command\" to be
`npm run build && npx convex deploy`.

`npx convex deploy` will read `CONVEX_DEPLOY_KEY` from the environment
and use that key to push your Convex functions to the *production*
deployment of this Convex project. This deployment has separate data
from the dev deployment used in `npx convex dev`.

Now, Convex has your newest functions and your app is configured to
connect to production. Lastly, the `npm run build` script bundles your
app and Netlify deploys it!

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)tip

</div>

<div>

If you\'re using Auth0 for authentication as outlined here, then you\'ll
need to update your Auth0 Application to include your new
`<site-name>.netlify.app` URL in the places where we specified
`localhost:3000` before. This way Auth0 allows this domain to receive
the authentication tokens.

</div>

</div>

</div>

</div>

</div>

</div>

</div>
