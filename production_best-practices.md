<div>

<div>

<div>

<div>

-   Home
-   Production
-   Best Practices

<div>

On this page

</div>

<div>

<div>

# Best Practices

</div>

Here\'s a collection of our recommendations on how best to use Convex to
build your application. If you want guidance specific to your app\'s
needs or have discovered other ways of using Convex, message us on
Discord!

## TypeScript​

**Use TypeScript!**

All Convex libraries have complete type annotations and using theses
types is a great way to learn the framework.

Even better, Convex supports code generation to create types that are
specific to your app\'s schema and Convex functions.

Code generation is run automatically by `npx convex dev`.

## Convex functions​

### Logging and debugging​

**Use `console.log` to debug your Convex functions.**

Any server-side log from a Convex query or mutation function will end up
both in the logs page in the dashboard, as well as in the browser
console logs for the user who invoked the function call.

If a server-side exception occurs, it will also be logged as an error
event which will appear in both places--- in the dashboard logs, and
echoed into the browser\'s console log.

### Data modeling​

**Use tables to separate logical object types.**

Even though Convex does support nested documents, it is often better to
put separate objects into separate tables and use `Id`s to create
references between them. This will give you more flexibility when
loading and querying documents.

You can read more about this at \[Document
IDs\]/docs/database/document-ids.md).

### Sharing Code​

**Use helper functions to write shared code.**

You can feel free to write additional helper functions in your `/convex`
directory and use them within your Convex functions. Helpers can be a
powerful way to share business logic, authorization code, and more.

### Prefer queries and mutations over actions​

You should generally avoid using actions when the same goal can be
achieved using queries or mutations. Since actions can have side
effects, they can\'t be automatically retried nor their results cached.
Actions should be used in more limited scenarios, such as calling
third-party services.

## UI patterns​

### Loading states​

**Check for `undefined` to determine if a query is loading.**

The `useQuery` React hook will return `undefined` when it is first
mounted, before the query has been loaded from Convex. Once a query is
loaded it will never be `undefined` again (even as the data reactively
updates). `undefined` is not a valid return type for queries (you can
see the types that Convex supports at Field Values)

You can use this as a signal for when to render loading indicators and
placeholder UI.

### Optimistic updates​

**Add optimistic updates for the interactions you want to feel snappy.**

By default all relevant `useQuery` hooks will update automatically after
a mutation is synced from Convex. If you would like some interactions to
happen even faster, you can add optimistic updates to your `useMutation`
calls so that the UI updates instantaneously.

### Error handling​

**Use an exception handling service and error boundaries to manage
errors.**

Inevitably, your Convex functions will have bugs and hit exceptions. If
you have an exception handling service and error boundaries configured,
you can ensure that you hear about these errors and your users see
appropriate UI.

See Error Handling for more information.

</div>

</div>

</div>

</div>

</div>
