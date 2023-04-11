<div>

<div>

<div>

<div>

<div>

On this page

</div>

<div>

<div>

# Get Started

</div>

You\'re just a few short steps away from building an interactive
live-updating web application entirely in JavaScript, all without
managing a backend. Follow along with the video or read on below.

## The backend-as-a-service for web applications​

Convex is a database and a backend-as-a-service for web applications.
Queries in Convex are full *JavaScript functions*, allowing you to
easily express your application logic. These queries can be used as
*end-to-end subscriptions* that update your React components in users\'
browsers whenever the data they depend on changes.

The best way to understand the magic of Convex is to see it in action.
We\'ll have you up and running in a manner of seconds...

## Your first Convex app​

Clone the starter project and install its dependencies.

<div>

<div>

    git clone https://github.com/get-convex/convex-tutorial.git
    cd convex-tutorial
    npm i

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This project contains a basic chat web app, including React code that
runs on the frontend and Convex query functions that run in the cloud.
`npm run dev` runs both the Convex dev server and a frontend dev server
to deploy and hot-reload both these functions and these Convex functions
and the application frontend.

<div>

<div>

    npm run dev

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)note

</div>

<div>

The first time you run this command you\'ll be prompted to log in via
GitHub and to create a new project. You don\'t need any additional
credentials or to pay for anything.

</div>

</div>

Your app is up and running.

## Convex reactivity​

Open another browser window with the same URL. You should see chat
messages typed in one browser window show up immediately in the other.
Any data in Convex (chat messages in this example app) will update
immediately for all viewers, anywhere in the world.

Open your project\'s dashboard to see your data. You can modify this
data directly, causing every browser window viewing the app to update
immediately.

### Hooking up React components​

Here\'s the first half of the code for the `App` React component of the
project you have running locally. React components communicate with the
Convex backend via the hooks `useQuery` and `useMutation`. This
component rerenders every time any user sends a new chat message.

<div>

<div>

src/App.jsx (excerpt)

</div>

<div>

    import { useMutation, useQuery } from "../convex/_generated/react";

    export default function App() {
      const messages = useQuery("listMessages") || [];

      const [newMessageText, setNewMessageText] = useState("");
      const sendMessage = useMutation("sendMessage");

      const [name] = useState(() => "User " + Math.floor(Math.random() * 10000));
      async function handleSendMessage(event) {
        event.preventDefault();
        setNewMessageText("");
        await sendMessage({ body: newMessageText, author: name });
      }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

In the three highlighted lines above:

-   `useQuery("listMessages")` returns either the result of running the
    `listMessages` query function on the server or `undefined` if the
    query result is still loading. This hook causes the component to
    rerender whenever the query result changes.
-   `useMutation("sendMessage")` returns a function for telling the
    server to run the `sendMessages` mutation.
-   `sendMessage({ body: newMessageText, author: name })` is called from
    an event handler, sending its arguments to the server so the
    `sendMessages` mutation function can be run with them.

### Query functions​

`"listMessages"` above refers to a query function: a JavaScript (or
TypeScript) function that runs on Convex servers. The first argument
passed to `useQuery` specifies the name of the file in the `convex/`
folder where this query function is the default export. This query
function returns every document in the messages table.

<div>

<div>

convex/listMessages.js

</div>

<div>

    import { query } from "./_generated/server";

    export default query(async ({ db }) => {
      return await db.query("messages").collect();
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Passing arguments to queries

<div>

<div>

As their first argument, query functions receive an object with a `db`
property that can be used to read from and write to Convex tables. You
can pass your own arguments to query functions by adding an arguments
object to the `useQuery` call.

<div>

<div>

    // src/App.jsx
    useQuery("listMessages", { maxMessages: 10, repeat: false });
                  │                │              └────--┐
                  │                └────--────┐          │
    // convex/listMessages.js                 │          │
    export default query(async ({ db }, { maxMessages, repeat }) => {
      // gets the latest maxMessages, ordered by most recent instead of earliest
      const messages = await db.query("messages").order("desc").take(maxMessages);
      // sort the messages back into chronological order
      messages.reverse();
      if (repeat) {
        return messages.map(m => {
          return {...m, body: `${m.body} ${m.body}`};
        };
      }
      return messages;
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

</div>

</div>

Breaking down the JavaScript syntax used here

<div>

<div>

In case the syntax of the query function in `convex/listMessages.js` is
unfamiliar let\'s break it down. Here\'s a simpler (and also totally
valid) way to write the same query function.

<div>

<div>

    const myFunction = async context => {
      const db = context.db;
      // Creates an array of all documents of the "messages" table
      // similar to `SELECT * FROM messages`
      const messages = await db.query("messages").collect();
      return messages;
    };
    const myQuery = query(myFunction);
    export default myQuery;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

We can use parameter destructuring to pull out `db` since that\'s the
only property of the query context object used in this function.

<div>

<div>

    const myFunction = async ({ db }) => {
      const messages = await db.query("messages").collect();
      return messages;
    };
    const myQuery = query(myFunction);
    export default myQuery;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Besides being one line shorter, calling `mutation()` directly on the
function we wrote helps code editors infer the types of its parameters.

<div>

<div>

    const myMutation = mutation(async ({ db }, { body, author }) => {
      const message = { body, author };
      await db.insert("messages", message);
    });
    export default myMutation;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Inlining the `export default` is just a preference. We could also
combine the middle two lines.

</div>

</div>

There\'s something special about query functions: they run
automatically! Every time data that would be read by a query function
changes, the function runs again and notifies all subscribed clients of
the change, causing the relevant React components to rerender with the
new query result.

Query functions are for more than returning collections of documents: in
addition to a querying the Convex database you can run any JavaScript
you need.

**How would you change this query function to\...**

Return chat messages without revealing their authors?

<div>

<div>

Query functions don\'t need to return documents from tables: they can
return modified documents or completely new objects. To avoid needing to
change the frontend code we can modify the `author` property in returned
messages instead of removing it.

<div>

<div>

    export default query(async ({ db }) => {
      const allMessages = await db.query("messages").collect();
      return allMessages.map(m => {
        return {
          ...m,
          author: "anonymous",
        };
      });
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

</div>

</div>

**How would you write a query function in a new JavaScript file in the
`convex/` folder\...**

called `getMessagesByAuthor.js` that returns only messages by a specific
author?

<div>

<div>

Since query functions are just JavaScript, array methods like filter are
often the simplest way to transform documents before returning them.
This is a great way to get started.

<div>

<div>

    export default query(async ({ db }, { author }) => {
      const allMessages = await db.query("messages").collect();
      return allMessages.filter(m => m.author === author);
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

You can use this new query in a React component with

<div>

<div>

    const ownMessages = useQuery("getMessagesByAuthor", name);

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

But as tables get larger, it\'s more efficient to use the query builder
to filter for the results we want instead processing an array containing
the entire table of documents in JavaScript.

<div>

<div>

    export default query(async ({ db }, { author }) => {
      return await db
        .table("messages")
        .filter(q => q.eq(q.field("author"), author))
        .collect();
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Using an index would be more efficient still.

</div>

</div>

called `getAuthors.js` that returns a list of authors and how many
messages they have posted?

<div>

<div>

<div>

<div>

    // convex/.js
    export default query(async ({ db }, { maxMessages }) => {
      const allMessages = await db.query("messages").collect();
      const authors = {};
      for (const message of allMessages) {
        authors[message.author] = (authors[message.authors] || 0) + 1;
      }
      return authors;
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

If you\'re thinking \"hmmm, it sounds like there should be two tables
here, one for messages and one for authors, with a foreign key in
messages to specify the author,\" you\'re not wrong. Convex works best
as a relational database!

See querying the database to learn about filters, references to
documents in other tables (AKA foreign keys), ordering results, and
indexes.

</div>

</div>

### Mutation functions​

Mutation functions are also normal JavaScript or TypeScript functions
that run on Convex servers when requested. Clicking the submit button in
our app tells the Convex backend to run the `sendMessage` mutation
function with the arguments provided.

<div>

<div>

convex/sendMessage.js

</div>

<div>

    import { mutation } from "./_generated/server";

    export default mutation(async ({ db }, { body, author }) => {
      const message = { body, author };
      await db.insert("messages", message);
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This mutation function creates an object with two properties, `body` and
`author`, and inserts that object into the messages table. Here\'s what
your dashboard might look like after sending a few messages from two
browser windows. You can see that documents in Convex tables get two
other properties for free: `_id` and `_creationTime`.

Since mutations are just JavaScript, see if you can figure out how to
make the following changes to the listMessages mutation function. If
`npx convex dev` is still running, changes you make to
`convex/listMessages.js` will be reflecting as soon as you save the
file.

**How would you change this mutation function\...**

to make every submitted chat messages ALL CAPS?

<div>

<div>

`body` is a string, so we can call `.toUpperCase()` on it to get the
shouty version.

<div>

<div>

    export default mutation(async ({ db }, { body, author }) => {
      const message = { body: body.toUpperCase(), author };
      await db.insert("messages", message);
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

</div>

</div>

to require messages to be longer than 10 characters?

<div>

<div>

Use an if statement! Remember, mutation functions are just JavaScript.

<div>

<div>

    export default mutation(async ({ db }, { body, author }) => {
      if (body.length < 10) {
        return "Message is not long enough!";
      }
      await db.insert("messages", { body: body.toUpperCase(), author });
      return "ok";
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Mutation functions can also return values back to the UI, so let\'s
modify the React component to do something with the result.

<div>

<div>

    // src/App.jsx
    const [errorMessage, setErrorMessage] = useState(null);
    async function handleSendMessage(event) {
      event.preventDefault();
      setNewMessageText("");
      const result = await sendMessage({ body: newMessageText, author: name });
      if (result === "ok") {
        setError(undefined);
      } else {
        setError(result);
      }
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

</div>

</div>

to prevent users from from spamming chat with too many messages? Hint:
mutations can read data too!

<div>

<div>

We can check the creation time of the last message sent by a user and
compare it with the current time. That might make you worry about race
conditions: could two messages slip in together, both reading the same
latest message? Don\'t worry, mutation functions run transactionally!

<div>

<div>

    export default mutation(async ({ db }, { body, author }) => {
      const now = Date.now();

      const allMessages = await db.query("messages").collect();
      const previousMessages = allMessages.filter(m => m.author === author);

      const lastMessageSent = Math.max(previousMessages.map(m => m._creationTime));
      if (lastMessageSent + 1000 * 10 > now) {
        return "Too soon to send a new message";
      }
      await db.insert("messages", { body: body.toUpperCase(), author });
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Being able to run arbitrary JavaScript in mutations and query functions
is powerful! But it\'s often more efficient to express filters like this
through the query builder, or even to use indexes (not shown here) to
avoid bringing every document in a table into memory.

<div>

<div>

    export default mutation(async ({ db }, { body, author }) => {
      const now = Date.now();

      const previousMessages = await db
        .table("messages")
        .filter(q => q.eq(q.field("author"), author))
        .collect();

      const lastMessageSent = Math.max(previousMessages.map(m => m._creationTime));
      if (lastMessageSent + 1000 * 10 > now) {
        return "Too soon to send a new message";
      }
      await db.insert("messages", { body: body.toUpperCase(), author });
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This is just the beginning of a rate limit: the most glaring issue with
it is that users could send in a different user name to evade it! To
prevent this you\'d want to add user authentication.

</div>

</div>

### The Convex client​

Back in the UI code, `useQuery()` and `useMutation()` could only be used
in the `App` component because a `ConvexProvider` above it in the React
component tree makes a `ConvexReactClient` instance available.

<div>

<div>

src/main.jsx

</div>

<div>

    import { StrictMode } from "react";
    import ReactDOM from "react-dom";
    import "./index.css";
    import App from "./App";
    import { ConvexProvider, ConvexReactClient } from "convex/react";

    const address = import.meta.env.VITE_CONVEX_URL;

    const convex = new ConvexReactClient(address);

    ReactDOM.render(
      <StrictMode>
        <ConvexProvider client={convex}>
          <App />
        </ConvexProvider>
      </StrictMode>,
      document.getElementById("root")
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

-   The url for a Convex deployment is retrieved from an environment
    variable. This URL might point to a production deployment in prod
    and your own personal development deployment when developing
    locally.
-   The `ConvexReactClient` constructor uses this URL to create a
    websocket connection to this server.
-   A `ConvexProvider` component uses a React context to provide all
    descendant React elements with this connection to the server.

## What next?​

This concludes a whirlwind tour of a Convex application: how to write
Convex functions and how to hook them up. If you haven\'t yet, do try
modifying the code: while `npx convex dev` is running, modifying a query
will update the results in your browser instantly. If you have any
trouble or want to ask questions, we\'re here to help.

<div>

<div>

## Functions

Write functions to define your server behavior.

</div>

<div>

## Database

Store JSON-like documents with a relational data model.

</div>

<div>

## File Storage

Store and serve files of any type.

</div>

<div>

## Users and Auth

Add authentication to your Convex app.

</div>

<div>

## Typescript

Move faster with end-to-end type safety.

</div>

<div>

## Deploying your project

Share your Convex backend and web app with the world.

</div>

</div>

</div>

</div>

</div>

</div>

</div>
