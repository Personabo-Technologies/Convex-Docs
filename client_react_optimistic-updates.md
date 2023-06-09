<div>

<div>

<div>

<div>

-   Home
-   Client Libraries
-   React
-   Optimistic Updates

<div>

On this page

</div>

<div>

<div>

# Optimistic Updates

</div>

Even though Convex queries are completely reactive, sometimes you\'ll
want to update your UI before the mutation changes propagate back to the
client. To accomplish this, you can configure an *optimistic update* to
execute as part of your mutation.

Optimistic updates are temporary, local changes to your query results
which are used to make your app more responsive. These updates are made
by functions registered on a mutation invocation with the
`.withOptimisticUpdate` configuration option.

Optimistic updates are run when a mutation is initiated, rerun if the
local query results change, and rolled back when a mutation completes.

## Simple example​

Here is how an optimistic update could be added to an `incrementCounter`
mutation in a simple counter app:

<div>

<div>

    const increment = useMutation("incrementCounter").withOptimisticUpdate(
      (localStore, increment) => {
        const currentValue = localStore.getQuery("getCounter", []);
        if (currentValue !== undefined) {
          localStore.setQuery("getCounter", [], currentValue + increment);
        }
      }
    );

    function incrementCounter() {
      return increment(1);
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Optimistic updates receive a `localStore`, a view of the Convex
client\'s internal state, followed by the arguments to the mutation.

This optimistic update updates the `getCounter` query to be `increment`
higher if it\'s loaded.

## Complex example​

If we want to add an optimistic update to a multi-channel chat app, that
might look like:

<div>

<div>

    const sendMessage = useMutation("sendMessage").withOptimisticUpdate(
      (localStore, channel, body) => {
        const existingMessages = localStore.getQuery("listMessages", [channel]);
        // If we've loaded the listMessages query, push an optimistic message
        // onto the list.
        if (existingMessages !== undefined) {
          const now = Date.now();
          const newMessage = {
            _id: new Id("messages", crypto.randomUUID()),
            _creationTime: now,
            channel,
            body,
          };
          localStore.setQuery(
            "listMessages",
            [channel],
            [...existingMessages, newMessage]
          );
        }
      }
    );

    async function handleSendMessage(channelId, newMessageText) {
      await sendMessage(channelId, newMessageText);
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This optimistic update changes the `listMessages` query for the current
channel to include a new message. The newly created message object
should match the structure of the real messages generated by the
`listMessages` query on the server.

Because this message includes the client\'s current time (not the
server\'s), it will inevitably not match the `listMessages` query after
the mutation runs. That\'s okay! The Convex client will handle rolling
back this update after the mutation completes and the queries are
updated. If there are small mistakes in optimistic updates, the UI will
always eventually render the correct values.

Similarly, the update creates a temporary `Id` with
`new Id("messages", crypto.randomUUID())`. This will also be rolled back
and replaced with the true ID once the server assigns it.

Lastly, note that this update creates a new array of messages instead of
using `existingMessages.push(newMessage)`. This is important! Mutating
objects inside of optimistic updates will corrupt the client\'s internal
state and lead to surprising results. Always create new objects inside
of optimistic updates.

## Learning more​

To learn more, check out our API documentation:

-   `.withOptimisticUpdate`
-   `OptimisticUpdate`
-   `OptimisticLocalStore`

If you\'d like some hands on experience, try adding optimistic updates
to the tutorial app! If you do, you should notice the app feels snappier
--- just a little, Convex is pretty fast already! --- but otherwise
works the same.

To explore even further, try inserting a mistake into this update! You
should see a flicker as the optimistic update is applied and then rolled
back.

</div>

</div>

</div>

</div>

</div>
