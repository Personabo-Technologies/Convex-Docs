<div>

<div>

<div>

<div>

-   Home
-   Client Libraries
-   React

<div>

On this page

</div>

<div>

<div>

# Convex React

</div>

Convex React is the client library enabling your React application to
interact with your Convex backend. It allows your frontend code to:

1.  Call your Queries, Mutations and Actions
2.  Upload and display files from File Storage
3.  Authenticate users using Authentication
4.  Implement full text Search over your data

## Installation​

Convex React is part of the `convex` npm package:

<div>

<div>

    npm install convex

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Connecting to a backend​

The `ConvexReactClient` maintains a connection to your Convex backend,
and is used by the React hooks described below to call your functions.

First you need to create an instance of the client by giving it your
backend deployment URL. See Configuring Deployment URL on how to pass in
the right value:

<div>

<div>

src/index.js

</div>

<div>

    import { ConvexProvider, ConvexReactClient } from "convex/react";
    const convex = new ConvexReactClient("https://<domain>.convex.cloud");

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

And then you make the client available to your app by passing it in to a
`ConvexProvider` wrapping your main component:

<div>

<div>

src/index.js

</div>

<div>

    reactDOMRoot.render(
      <React.StrictMode>
        <ConvexProvider client={convex}>
          <App />
        </ConvexProvider>
      </React.StrictMode>
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Fetching data​

Your React app fetches data using the `useQuery` React hook by calling
your queries.

The `convex dev` command generates this hook for you in the
`convex/_generated/react.js` module to provide better autocompletion in
JavaScript and end-to-end type safety in TypeScript:

<div>

<div>

src/App.js

</div>

<div>

    import { useQuery } from "../convex/_generated/react";

    export function App() {
      const data = useQuery("myQuery");
      return data ?? "Loading...";
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

The `useQuery` hook returns `undefined` while the data is first loading
and afterwards the return value of your query.

### Query arguments​

Arguments to your query follow the query name:

<div>

<div>

src/App.js

</div>

<div>

    export function App() {
      const a = "Hello world";
      const b = 4;
      const data = useQuery("myQuery", { a, b });
      …

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Reactivity​

The `useQuery` hook makes your app automatically reactive: when the
underlying data changes in your database, your component rerenders with
the new query result.

The first time the hook is used it creates a subscription to your
backend for a given query and any arguments you pass in. When your
component unmounts, the subscription is cancelled.

### Consistency​

Convex React ensures that your application always renders a consistent
view of the query results based on a single state of the underlying
database.

Imagine a mutation changes some data in the database, and that 2
different `useQuery` call sites rely on this data. Your app will never
render in an inconsistent state where only one of the `useQuery` call
sites reflects the new data.

## Editing data​

Your React app edits data using the `useMutation` React hook by calling
your mutations.

The `convex dev` command generates this hook for you in the
`convex/_generated/react.js` module to provide better autocompletion in
JavaScript and end-to-end type safety in TypeScript:

<div>

<div>

src/App.js

</div>

<div>

    import { useMutation } from "../convex/_generated/react";

    export function App() {
      const doSomething = useMutation("doSomething");
      return <button onClick={() => doSomething()}>Click me</button>;
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

The hook returns an `async` function which performs the call to the
mutation.

### Mutation arguments​

Arguments to your mutation are passed to the `async` function returned
from `useMutation`:

<div>

<div>

src/App.js

</div>

<div>

    export function App() {
      const a = "Hello world";
      const b = 4;
      const doSomething = useMutation("doSomething");
      return <button onClick={() => doSomething({ a, b })}>Click me</button>;
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Mutation response and error handling​

The mutation can optionally return a value or throw errors, which you
can `await`:

<div>

<div>

src/App.js

</div>

<div>

    export function App() {
      const doSomething = useMutation("doSomething");
      const onClick = () => {
        async function callBackend() {
          try {
            const result = await doSomething();
          } catch (error) {
            console.error(error);
          }
          console.log(result);
        }
        callBackend();
      };
      return <button onClick={onClick}>Click me</button>;
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Or handle as a `Promise`:

<div>

<div>

src/App.js

</div>

<div>

    export function App() {
      const doSomething = useMutation("doSomething");
      const onClick = () => {
        doSomething()
          .catch(error => {
            console.error(error);
          })
          .then(result => {
            console.log(result);
          });
      };
      return <button onClick={onClick}>Click me</button>;
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Learn more about Error Handling in functions.

### Retries​

Convex React automatically retries mutations until they are confirmed to
have been written to the database. The Convex backend ensures that
despite multiple retries, every mutation call only executes once.

Additionally, Convex React will warn users if they try to close their
browser tab while there are outstanding mutations. This means that when
you call a Convex mutation, you can be sure that the user\'s edits
won\'t be lost.

### Optimistic updates​

Convex queries are fully reactive, so all query results will be
automatically updated after a mutation. Sometimes you may want to update
the UI before the mutation changes propagate back to the client. To
accomplish this, you can configure an *optimistic update* to execute as
part of your mutation.

Optimistic updates are temporary, local changes to your query results
which are used to make your app more responsive.

See Optimistic Updates on how to configure them.

## Calling third-party APIs​

Your React app can read data, call third-party services, and write data
with a single backend call using the `useAction` React hook by calling
your actions.

The `convex dev` command generates this hook for you in the
`convex/_generated/react.js` module to provide better autocompletion in
JavaScript and end-to-end type safety in TypeScript:

<div>

<div>

src/App.js

</div>

<div>

    import { useAction } from "../convex/_generated/react";

    export function App() {
      const doSomeAction = useAction("actions/doSomeAction");
      return <button onClick={() => doSomeAction()}>Click me</button>;
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

The hook returns an `async` function which performs the call to the
action.

### Action arguments​

Action arguments work exactly the same as mutation arguments.

### Action response and error handling​

Action response and error handling work exactly the same as mutation
response and error handling.

Actions do not support automatic retries or optimistic updates.

## Under the hood​

The `ConvexReactClient` connects to your Convex deployment by creating a
`WebSocket`. The WebSocket provides a 2-way communication channel over
TCP. This allows Convex to push new query results reactively to the
client without the client needing to poll for updates.

If the internet connection drops, the client will handle reconnecting
and re-establishing the Convex session automatically.

</div>

</div>

</div>

</div>

</div>
