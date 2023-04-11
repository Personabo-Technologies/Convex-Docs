<div>

<div>

<div>

<div>

-   Home
-   Database
-   Writing Data

<div>

On this page

</div>

<div>

<div>

# Writing Data

</div>

Mutations can insert, update, and remove data from database tables.

## Inserting new documents​

You can create new documents in the database with the `db.insert`
method:

<div>

<div>

    export default mutation(async ({ db }, { name }) => {
      const taskId = await db.insert("tasks", { name });
      …

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

The second argument to `db.insert` is a JavaScript object with data for
the new document.

The same types of values that can be passed into and returned from
queries and mutations can be written into the database. See Field Values
for the full list of supported types.

The `insert` method returns a globally unique ID for the newly inserted
document.

## Updating existing documents​

Given an existing document ID the document can be updated using the
following methods:

1.  The `db.patch` method will add new fields and override existing
    fields of the existing document:

<div>

<div>

    export default mutation(async ({ db }, { id, tag }) => {
      const task = await db.get(id);
      console.log(task); // prints {name: "Foo"}
      await db.patch("tasks", id, {tag});
      const task = await db.get(id);
      console.log(task); // prints {name: "Foo", tag: "Bar"}
      …

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

1.  The `db.replace` method will replace the existing document entirely,
    potentially removing existing fields:

<div>

<div>

    export default mutation(async ({ db }, { id, tag }) => {
      const task = await db.get(id);
      console.log(task); // prints {name: "Foo"}
      await db.replace("tasks", id, {tag});
      const task = await db.get(id);
      console.log(task); // prints {tag: "Bar"}
      …

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Deleting documents​

Given an existing document ID the document can be removed from the table
with the `db.delete` method.

<div>

<div>

    export default mutation(async ({ db }, { id }) => {
      await db.delete(id);
    });

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>
