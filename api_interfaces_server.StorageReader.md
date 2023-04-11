<div>

<div>

<div>

<div>

-   Home
-   API reference
-   Convex API
-   convex/server
-   StorageReader

<div>

On this page

</div>

<div>

<div>

# Interface: StorageReader

</div>

server.StorageReader

An interface to read from storage within Convex query functions.

## Hierarchy​

-   **`StorageReader`**

    ↳ `StorageWriter`

## Methods​

### getUrl​

▸ **getUrl**(`storageId`): `Promise`\<`null` \| `string`\>

Get the URL for a file in storage by its StorageId.

The GET response includes a standard HTTP Digest header with a sha256
checksum.

#### Parameters​

  Name          Type       Description
  ------------- ---------- ---------------------------------------------------------
  `storageId`   `string`   The StorageId of the file to fetch from Convex storage.

#### Returns​

`Promise`\<`null` \| `string`\>

-   A url which fetches the file via an HTTP GET, or `null` if it no
    longer exists.

------------------------------------------------------------------------

### getMetadata​

▸ **getMetadata**(`storageId`): `Promise`\<`null` \| `FileMetadata`\>

Get metadata for a file.

#### Parameters​

  Name          Type       Description
  ------------- ---------- ----------------------------
  `storageId`   `string`   The StorageId of the file.

#### Returns​

`Promise`\<`null` \| `FileMetadata`\>

-   A FileMetadata object if found or `null` if not found.

</div>

</div>

</div>

</div>

</div>
