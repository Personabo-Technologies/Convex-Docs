<div>

<div>

<div>

<div>

-   Home
-   API reference
-   HTTP API

<div>

On this page

</div>

<div>

# Sync APIs

Convex supports both streaming export and streaming import via Airbyte.

## Authorization​

Streaming export and streaming import requests require the HTTP header
`Authorization`. The value is `Convex <access_key>` where the access key
comes from \"Deploy key\" on the Convex dashboard and gives full read
and write access to your Convex data.

## Streaming Export​

Sign up for a Professional plan for streaming export support. Read more
about using streaming export with Airbyte here.

### Format​

Each of the streaming export APIs take a `format` query param that
describes how documents are formatted. Currently the only supported
value is `convex_json`, which encodes documents with enough information
to determine the original type.

For example, floats (JavaScript `number`) are represented as JSON
numbers, so integers are represented as `{"$int": "<base64 integer>"}`.
Similarly, arrays are represented as JSON arrays, so sets (JavaScript
`Set`) are represented as `{"$set": [<values>]}`.

### GET `/api/json_schemas`​

The JSON Schemas endpoint lists tables, and for each table describes how
documents will be encoded, given as JSON Schema. This endpoint returns
`$description` tags throughout the schema to describe unintuitive
encodings and give extra information like the table referenced by `Id`
fields.

An additional query param `deltaSchema=true` shows extra fields returned
by `/api/document_deltas` and `/api/list_snapshot` for each document.
These fields are metadata about what has changed about the document: the
timestamp `_ts` and whether the document was deleted `_deleted`.

### GET `/api/list_snapshot`​

The `list_snapshot` endpoint walks a consistent snapshot of documents.

The `tableName` query param filters to a table. If omitted,
`list_snapshot` returns documents from all tables.

Expected API usage:

1.  Call `/api/list_snapshot` with no extra arguments (just `format` and
    optionally `tableName`).
2.  Get a page of documents from the response\'s `values` field.
3.  If the response\'s `hasMore` field is false, `break`. We have listed
    the full snapshot and can move on to document deltas.
4.  Record the response\'s `snapshot` and `cursor` fields.
5.  Call `/api/list_snapshot?snapshot=$snapshot&cursor=$cursor`, passing
    in the snapshot and cursor from the response to get the next page of
    documents.
6.  Go to step 2.

### GET `/api/document_deltas`​

The `document_deltas` endpoint walks the change log of documents to find
new, updated, and deleted documents in the order of their mutations.
This order is given by a `_ts` field on the returned documents.
Deletions are represented as JSON objects with fields `_id`, `_ts`, and
`_deleted: true`.

Expected API usage:

1.  Sync a full snapshot by calling `list_snapshot` until `hasMore` is
    false.
2.  Record snapshot from the `list_snapshot` response as the new
    `cursor`. The delta walk will start at this timestamp.
3.  Call `/api/document_deltas?cursor=$cursor` (also with arguments
    `format` and optionally `tableName`)
4.  Get a page of documents from the response\'s `values` field.
5.  If the response\'s `hasMore` field is false, `break`. We are now
    caught up.
    -   Save the most recent `cursor` to begin the next incremental sync
        with a `document_deltas` call.
6.  Record the response\'s `cursor` field.
7.  Go to step 3.

## Streaming Import​

Streaming import support is automatically enabled for all Convex
projects.

### Headers​

Streaming import endpoints accept a
`Convex-Client: streaming-import-<version>` header, where the version
follows Semver guidelines. If this header is not specified, Convex will
default to the latest version. We recommend using the header to ensure
the consumer of this API does not break as the API changes.

### GET `/api/streaming_import/primary_key_indexes_ready`​

The `primary_key_indexes_ready` endpoint takes a list of table names and
returns true if the primary key indexes (created by
`add_primary_key_indexes`) on all those tables are ready. If the tables
are newly created, the indexes should be ready immediately; however if
there are existing documents in the tables, it may take some time to
backfill the primary key indexes. The response looks like:

<div>

<div>

    {
      "indexesReady": true
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### PUT `/api/streaming_import/add_primary_key_indexes`​

The `add_primary_key_indexes` endpoint takes a JSON body containing the
primary keys for tables and creates indexes on the primary keys to be
backfilled. Note that they are not immediately ready to query - the
`primary_key_indexes_ready` endpoint needs to be polled until it returns
True before calling `import_airbyte_records` with records that require
primary key indexes. Also note that Convex queries will not have access
to these added indexes. These are solely for use in
`import_airbyte_records`. The body takes the form of a map of index
names to list of field paths to index. Each field path is represented by
a list of fields that can represent nested field paths.

<div>

<div>

    {
      "indexes": {
        "<table_name>": [["<field1>"], ["<field2>", "<nested_field>"]]
      }
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Expected API Usage:

1.  Add indexes for primary keys by making a request to
    `add_primary_key_indexes`.
2.  Poll `primary_key_indexes_ready` until the response is true.
3.  Query using the added indexes.

### PUT `api/streaming_import/clear_tables`​

This endpoint is deprecated. Use `api/streaming_import/replace_tables`
instead.

The `clear_tables` endpoint deletes all documents from the specified
tables. Note that this may require multiple transactions. If there is an
intermediate error only some documents may be deleted. The JSON body to
use this API request contains a list of table names:

<div>

<div>

    {
      "tableNames": ["<table_1>", "<table_2>"]
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### POST `api/streaming_import/replace_tables`​

The `replace_tables` endpoint renames tables with temporary names to
their final names, deleting any existing tables with the final names.

The JSON body to use this API request contains a list of table names:

<div>

<div>

    {
      "tableNames": { "<table_1_temp>": "<table_1>", "<table_2_temp>": "<table_2>" }
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### POST `api/streaming_import/import_airbyte_records`​

The `import_airbyte_records` endpoint enables streaming ingress into a
Convex deployment and is designed to be called from an Airbyte
destination connector.

It takes a map of streams and a list of messages in the JSON body. Each
stream has a name and JSON schema that will correspond to a Convex
table. Streams where records should be deduplicated include a primary
key as well, which is represented as a list of lists of strings that are
field paths. Records for streams without a primary key are appended to
tables; records for streams with a primary key replace an existing
record where the primary key value matches or are appended if there is
no match. If you are using primary keys, you must call the
`add_primary_key_indexes` endpoint first and wait for them to backfill
by polling `primary_key_indexes_ready`.

Each message contains a stream name and a JSON document that will be
inserted (or replaced, in the case of deduplicated sync) into the table
with the corresponding stream name. Table names are same as the stream
names. Airbyte records become Convex documents.

<div>

<div>

    {
       "tables": {
          "<stream_name>": {
             "primaryKey": [["<field1>"], ["<field2>", "<nested_field>"]],
             "jsonSchema": // see https://json-schema.org/ for examples
          }
       },
       "messages": [{
          "tableName": "<table_name>",
          "data": {} // JSON object conforming to the `json_schema` for that stream
       }]
    }

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Similar to `clear_tables`, it is possible to execute a partial import
using `import_airbyte_records` if there is a failure after a transaction
has committed.

Expected API Usage:

1.  \[Optional\] Add any indexes if using primary keys and deduplicated
    sync (see `add_primary_key_indexes` above).
2.  Make a request to `import_airbyte_records` with new records to sync
    and stream information.
3.  \[Optional\] Replace tables with temp tables using `replace_tables`
    if using overwrite sync.

</div>

</div>

</div>

</div>

</div>
