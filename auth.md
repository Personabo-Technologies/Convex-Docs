<div>

<div>

<div>

<div>

<div>

<div>

# Authentication

</div>

Authentication allows you to identify users and restrict what data they
can see and edit.

Your product will need a way for users to sign up, log in, log out and,
if passwords are used, a way to recover access after losing a password.
This is a complicated feature set to implement, especially given that
any bugs impact security.

You can implement all of this using Convex, but we currently recommend
that you instead leverage a Convex integration with an existing
third-party auth provider. This will be much less work and a more secure
solution. Choose from one of the following integrations, which both
provide login via passwords, social identity providers and one-time
email or SMS access codes:

-   Clerk is newer and has better Next.js and React Native support
-   Auth0 is more established with more bells and whistles

You could also only leverage social identity providers directly, such as
Google, Facebook, Apple or Github. Each provider has a different way to
integrate their service though, and in general this is more complicated
than using the integrations above.

Custom Auth Integration describes how you can integrate an identity
provider on your own.

</div>

</div>

</div>

</div>

</div>
