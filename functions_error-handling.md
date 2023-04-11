<div>

<div>

<div>

<div>

-   Home
-   Functions
-   Error Handling

<div>

On this page

</div>

<div>

<div>

# Error Handling

</div>

There are two reasons why your Convex queries and mutations may hit
errors:

1.  Developer Errors: There is a bug in the function (like calling
    `db.get(null)` instead of `db.get(id)`).
2.  Internal Convex Errors: There is a problem within Convex (like a
    network blip).

Convex will automatically handle internal Convex errors. If there are
problems on our end, we\'ll automatically retry your queries and
mutations until the problem is resolved and your queries and mutations
succeed.

On the other hand, you must decide how to handle developer errors. When
a developer error happens, the best practices are to:

1.  Show the user some appropriate UI.
2.  Send the error to an exception reporting service like Sentry so that
    you can follow up and fix the bug.

This guide provides advice on how to do both of these things.

## Errors in queries​

If your query function hits an error, the error will be sent to the
client and thrown from your `useQuery` call site. **The best way to
handle these errors is with a React error boundary component.**

Error boundaries allow you to catch errors thrown in their child
component tree, render fallback UI, and send information about the error
to your exception handling service. Adding error boundaries to your app
is a great way to handle errors in Convex query functions as well as
other errors in your React components. If you are using Sentry, you can
use their `Sentry.ErrorBoundary` component.

With error boundaries, you can decide how granular you\'d like your
fallback UI to be. Once simple option is to wrap your entire application
in a single error boundary like:

<div>

<div>

    <StrictMode>
      <ErrorBoundary>
        <ConvexProvider client={convex}>
          <App />
        </ConvexProvider>
      </ErrorBoundary>
    </StrictMode>,

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Then any error in any of your components will be caught by the boundary
and render the same fallback UI.

On the other hand, if you\'d like to enable some portions of your app to
continue functioning even if other parts hit errors, you can instead
wrap different parts of your app in separate error boundaries.

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)Retrying

</div>

<div>

Unlike other frameworks, there is no concept of \"retrying\" if your
query function hits a developer error. Because Convex functions are
deterministic, if the query function hits an error, retrying will always
produce the same error. There is no point in running the query function
with the same arguments again.

</div>

</div>

## Errors in mutations​

If a mutation hits an error, this will

1.  Cause the promise returned from your mutation call to be rejected.
2.  Cause your optimistic update to be rolled back.

If you have an exception service like Sentry configured, it should
report \"unhandled promise rejections\" like this automatically. That
means that with no additional work your mutation errors should be
reported.

Note that errors in mutations won\'t be caught by your error boundaries
because the error doesn\'t happen as part of rendering your components.

If you would like to render UI specifically in response to a mutation
failure, you can use `.catch` on your mutation call. For example:

<div>

<div>

    sendMessage(newMessageText).catch(error => {
      // Do something with your error here.
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

If you\'re using an `async` handled function you can also use
`try...catch`:

<div>

<div>

    try {
      await sendMessage(newMessageText);
    } catch {
      // Do something with your error here.
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

<div>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)Reporting
caught errors

</div>

<div>

If you handle your mutation error, it will no longer become an unhandled
promise rejection. You may need to report this error to your exception
handling service manually.

</div>

</div>

## Errors in action functions​

Unlike queries and mutations, actions may have side-effects and
therefore can\'t be automatically retried by Convex when errors occur.
For example, say your action sends a email. If it fails part-way
through, Convex has no way of knowing if the email was already sent and
can\'t safely retry the action. It is responsibility of the caller to
handle errors raised by actions and retry if appropriate.

## Expected failures​

If you have common ways that you expect your query and mutations to
fail, it\'s often simpler to use TypeScript union return types to
communicate these cases instead of exceptions.

For example, a `createUser` mutation could return
`Id | "EMAIL_ADDRESS_IN_USE"` to express that either the mutation
succeeded or the email address was already taken.

This ensures that you remember to handle these cases in your UI. It also
saves errors for unexpected bugs that should be fixed.

</div>

</div>

</div>

</div>

</div>
