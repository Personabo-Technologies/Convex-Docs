<div>

<div>

<div>

<div>

-   Home
-   Production
-   Hosting and Deployment
-   Vercel

<div>

On this page

</div>

<div>

<div>

# Using Convex with Vercel

</div>

**New to Convex?** Convex is the reactive backend-as-a-service for web
developers. Convex allows you to define your backend with JavaScript
functions that push updates your React components in realtime. To get
started, head to the tutorial or the homepage.

Hosting your Convex app on Vercel allows you to automatically re-deploy
both your backend and your frontend whenever you push to git.

## Deploying to Vercel​

If you haven\'t done so, create a Vercel account. This is free for small
projects and should take less than a minute to set up. When asked to
deploy a first project just click the link to skip that step for now.

Once you have a working project that runs locally and have created a
GitHub repo for it, create a project at https://vercel.com/new and link
the project to the source code repository.

We need to make two changes from the Vercel defaults.

First, go into \"Build and Output Settings\" and **override the \"Build
Command\" to be `npm run build && npx convex deploy`**. We\'ll discuss
why this is necessary in a bit.

Second, let\'s **add a Convex deploy key as an environment variable**:

1.  Go to the Convex Dashboard.
2.  Find your project and click \"Settings\".
3.  Copy the \"Deploy key\".
4.  In Vercel, click \"Environment Variables\".
5.  Add an environment variable with the name `CONVEX_DEPLOY_KEY` and
    paste the deploy key as the value.

If your Convex project is nested under a subdirectory you\'ll also need
to change \"Root Directory\" accordingly.

Click the **Deploy** button and your work here is done!

Vercel will automatically publish your site to an URL like
`https://<site-name>.vercel.app`, shown on the page after deploying.
Every time you push a git revision, Vercel will automatically deploy
your Convex functions and publish your site changes.

## How it works​

In Vercel, we overrode the \"Build Command\" to be
`npm run build && npx convex deploy`.

`npx convex deploy` will read `CONVEX_DEPLOY_KEY` from the environment
and use that key to push your Convex functions to the *production*
deployment of this Convex project. This deployment has separate data
from the dev deployment used in `npx convex dev`.

Now, Convex has your newest functions and your app is configured to
connect to production. Lastly, the `npm run build` script bundles your
app and Vercel deploys it!

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)tip

</div>

<div>

If you\'re using Auth0 for authentication as we outline here, then
you\'ll need to update your Auth0 Application to include your new
`<site-name>.vercel.app` URL in the places where we specified
`localhost:3000` before. This way Auth0 allows this domain to receive
the authentication tokens.

</div>

</div>

</div>

</div>

</div>

</div>

</div>
