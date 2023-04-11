<div>

<div>

<div>

<div>

<div>

<div>

# Functions

</div>

Functions run on the backend and are written in JavaScript (or
TypeScript). They are automatically available as APIs accessed through
client libraries. Everything you do in the Convex backend starts from
functions.

There are three types of functions: queries, mutations, and actions.
Queries and mutations are how you access the database, and actions are
how you talk to external services and APIs.

-   Queries are automatically cached and subscribable. They have read
    access to the Convex database and don\'t have side effects. Query
    functions allow you to keep every device connected to your backend
    up to date.
-   Mutations have read & write access to the database and run in a
    transaction. Like queries, mutations don\'t have side effects
    besides writing to the database.
-   Actions can talk to the rest of the world. This allows you to
    connect to Open AI, Stripe, Twilio, or any other service or API you
    need to make your app work. Actions talk to the database by running
    query or mutation functions.

Convex also lets you build HTTP endpoints when you want to call your
functions from a webhook or a custom client.

</div>

</div>

</div>

</div>

</div>
