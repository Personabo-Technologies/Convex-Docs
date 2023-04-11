<div>

<div>

<div>

<div>

-   Home
-   Database
-   Field Values

<div>

On this page

</div>

<div>

<div>

# Field Values

</div>

All Convex documents are defined as Javascript objects. These objects
can have field values of any of the types below.

You can codify the shape of documents within your tables by defining a
schema.

## Convex values​

Convex supports the following types of values:

+-----------------+-----------------+-----------------+-----------------+
| Convex Type     | JavaScript Type | <div>           | Notes           |
|                 |                 |                 |                 |
|                 |                 | Example Usage   |                 |
|                 |                 |                 |                 |
|                 |                 | </div>          |                 |
+=================+=================+=================+=================+
| Id              | Id              | `doc._id`\      | See \[Document  |
|                 |                 | `new Id(        | IDs\]/d         |
|                 |                 | tableName, id)` | ocs/database/do |
|                 |                 |                 | cument-ids.md). |
+-----------------+-----------------+-----------------+-----------------+
| Null            | null            | `null`          | JavaScript\'s   |
|                 |                 |                 | `undefined` is  |
|                 |                 |                 | not a valid     |
|                 |                 |                 | Convex value.   |
|                 |                 |                 | Use `null`      |
|                 |                 |                 | instead.        |
+-----------------+-----------------+-----------------+-----------------+
| Int64           | bigint          | `3n`            | Int64s only     |
|                 |                 |                 | support BigInts |
|                 |                 |                 | between -2\^63  |
|                 |                 |                 | and 2\^63-1.    |
|                 |                 |                 | Convex supports |
|                 |                 |                 | `bigint`s in    |
|                 |                 |                 | most modern     |
|                 |                 |                 | browsers.       |
+-----------------+-----------------+-----------------+-----------------+
| Float64         | number          | `3.1`           | Convex supports |
|                 |                 |                 | all IEEE-754    |
|                 |                 |                 | d               |
|                 |                 |                 | ouble-precision |
|                 |                 |                 | floating point  |
|                 |                 |                 | numbers (such   |
|                 |                 |                 | as NaNs).       |
+-----------------+-----------------+-----------------+-----------------+
| Boolean         | boolean         | `true`          |                 |
+-----------------+-----------------+-----------------+-----------------+
| String          | string          | `"abc"`         | Strings are     |
|                 |                 |                 | stored as UTF-8 |
|                 |                 |                 | and must be     |
|                 |                 |                 | valid Unicode   |
|                 |                 |                 | sequences.      |
|                 |                 |                 | Strings must be |
|                 |                 |                 | smaller than    |
|                 |                 |                 | the 1MB total   |
|                 |                 |                 | size limit when |
|                 |                 |                 | encoded as      |
|                 |                 |                 | UTF-8.          |
+-----------------+-----------------+-----------------+-----------------+
| Bytes           | ArrayBuffer     | `new            | Convex supports |
|                 |                 | ArrayBuffer(8)` | first class     |
|                 |                 |                 | bytestrings,    |
|                 |                 |                 | passed in as    |
|                 |                 |                 | `ArrayBuffer`s. |
|                 |                 |                 | Bytestrings     |
|                 |                 |                 | must be smaller |
|                 |                 |                 | than the 1MB    |
|                 |                 |                 | total size      |
|                 |                 |                 | limit for       |
|                 |                 |                 | Convex types.   |
+-----------------+-----------------+-----------------+-----------------+
| Array           | Array           | `[              | Arrays can have |
|                 |                 | 1, 3.2, "abc"]` | at most 1024    |
|                 |                 |                 | values.         |
+-----------------+-----------------+-----------------+-----------------+
| Set             | Set             | `new Set([1     | Sets store only |
|                 |                 | , 3.2, "abc"])` | unique values.  |
|                 |                 |                 | Sets can have   |
|                 |                 |                 | at most 1024    |
|                 |                 |                 | values.         |
+-----------------+-----------------+-----------------+-----------------+
| Map             | Map             | `new Map([      | Maps support    |
|                 |                 | ["a", "abc"]])` | arbitrary       |
|                 |                 |                 | Convex types as |
|                 |                 |                 | keys, where     |
|                 |                 |                 | objects can     |
|                 |                 |                 | only have       |
|                 |                 |                 | strings for     |
|                 |                 |                 | field names.    |
|                 |                 |                 | Maps can have   |
|                 |                 |                 | at most 1024    |
|                 |                 |                 | values.         |
+-----------------+-----------------+-----------------+-----------------+
| Object          | object          | `{a: "abc"}`    | Convex only     |
|                 |                 |                 | supports        |
|                 |                 |                 | \"plain old     |
|                 |                 |                 | JavaScript      |
|                 |                 |                 | objects\"       |
|                 |                 |                 | (objects that   |
|                 |                 |                 | do not have a   |
|                 |                 |                 | custom          |
|                 |                 |                 | prototype).     |
|                 |                 |                 | Convex includes |
|                 |                 |                 | all enumerable  |
|                 |                 |                 | properties.     |
|                 |                 |                 | Objects can     |
|                 |                 |                 | have at most    |
|                 |                 |                 | 1024 entries.   |
|                 |                 |                 | Field names     |
|                 |                 |                 | must be         |
|                 |                 |                 | nonempty and    |
|                 |                 |                 | not start with  |
|                 |                 |                 | \"\$\" or       |
|                 |                 |                 | \"\_\".         |
+-----------------+-----------------+-----------------+-----------------+

## System fields​

Every document in Convex has two automatically-generated system fields:

-   `_id`: The \[document ID\]/docs/database/document-ids.md) of the
    document.
-   `_creationTime`: The time this document was created, in milliseconds
    since the Unix epoch.

## Limits​

Convex values must be less than 1MB in total size. This is an
approximate limit for now, but if you\'re running into these limits and
would like a more precise method to calculate a document\'s size, reach
out to us. Documents can have nested values, such as objects, maps,
sets, and arrays that contain other Convex types. Convex types can have
at most 16 levels of nesting, and the cumulative size of a nested tree
of values must be under the 1MB limit.

Table names may contain alphanumeric characters (\"a\" to \"z\", \"A\"
to \"Z\", and \"0\" to \"9\") and underscores (\"\_\"), and they cannot
start with an underscore.

If any of these limits don\'t work for you, let us know!

</div>

</div>

</div>

</div>

</div>
