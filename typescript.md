<div>

<div>

<div>

<div>

<div>

On this page

</div>

<div>

<div>

# TypeScript

</div>

**Example:** TypeScript and Schema

Convex provides end-to-end type support when Convex functions are
written in TypeScript.

You can gradually add TypeScript to a Convex project: the following
steps provide progressively better type support. For the best support
you\'ll want to complete them all.

### Writing Convex functions in TypeScript​

The first step to improving type support in a Convex project is to
writing your Convex functions in TypeScript. TypeScript inference is so
good that the difference between writing a Convex function in JavaScript
and TypeScript may be very small! Start by renaming the convex module
from e.g. `addChannel.js` to `addChannel.ts` and add annotations for
function parameters.

<div>

<div>

    import { mutation } from "./_generated/server";

    export default mutation(
      // The only change required to convert this function to
      // TypeScript is annotating the type of the arguments object.
      async ({ db }, { name }: { name: string }) => {
        return db.insert("channels", { name });
      }
    );

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

If TypeScript is installed in your project `npx convex dev` and
`npx convex deploy` will typecheck Convex functions before sending code
to the Convex backend.

Convex functions are typechecked with the `tsconfig.json` in the Convex
folder: you can modify some parts of this file to change typechecking
settings, or delete this file to disable this typecheck.

You\'ll find most database methods have a return type of `Promise<any>`
until you add a schema.

### Adding a schema​

Once you define a schema the type signature of database methods will be
known. You\'ll also be able to use types imported from
`convex/_generated/dataModel` in both Convex functions and application
code.

The types of documents in tables can be described using `Doc` from the
generated data model and references to documents can be described with
parametrized \[Document IDs\]/docs/database/document-ids.md).

<div>

<div>

    import { Doc, Id } from "../convex/_generated/dataModel";

    function Channel(props: { channelId: Id<"channels"> }) { ... }
    function MessagesView(props: { message: Doc<"messages"> }) { ... }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Writing frontend code in TypeScript​

Invocations of `useQuery` and `useMutation` the signatures of their
corresponding Convex functions. For end to end type safety, install and
configure TypeScript so you can write your React components in `.tsx`
files instead of `.jsx` files.

### Recommended TypeScript version​

Convex works best with TypeScript version 4.8.4 or newer.

</div>

</div>

</div>

</div>

</div>
