<div>

<div>

<div>

<div>

-   Home
-   Database
-   Tables & Documents

<div>

On this page

</div>

<div>

<div>

# Tables & Documents

</div>

## Tables​

Your Convex deployment contains tables that hold your app\'s data.
Initially, your deployment contains no tables or documents.

Each table springs into existence as soon as you add the first document
to it.

<div>

<div>

    // `friends` table doesn't exist.
    await db.insert("friends", { name: "Jamie" });
    // Now it does, and it has one document.

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

You do not have to specify a schema up front or create tables
explicitly.

## Documents​

Tables contain documents. Documents are very similar to JavaScript
objects. They have fields and values, and you can nest arrays or objects
within them.

These are all valid Convex documents:

<div>

<div>

    {}
    {"name": "Jamie"}
    {"name": {"first": "Arnold", "second": "Cole": 61}

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

They can also contain references to other documents in other tables. See
Field Values to learn more about the types supported in Convex and
Document IDs to learn about how to use those types to model your data.

</div>

</div>

</div>

</div>

</div>
