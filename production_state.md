<div>

<div>

<div>

<div>

-   Home
-   Production
-   Status and Guarantees

<div>

On this page

</div>

<div>

<div>

# Status and Guarantees

</div>

Convex is ready for production use. You can choose a plan that\'s right
for you.

Please contact us with any specific requirements or if you want to build
a project on Convex that is not yet satisfied by our guarantees.

## Guarantees​

The official Convex Terms of Service, Privacy Policy and Customer
Agreements are outlined in our official terms. We do not yet have
contractual agreements beyond what is listed in our official terms and
the discussions within this document don\'t constitute an amendment to
these terms.

Convex is pre-1.0, which means we may still make breaking changes to our
API. You can follow along with the updates on our blog. We will use our
best effort to avoid major breaking changes, and you can skip an update
for a limited period of time if you want more time to update to a newer
API.

All user data in Convex is encrypted at rest. Database state is
replicated durably across multiple physical availability zones. Regular
periodic and incremental database backups are performed and stored with
99.999999999% (11 9\'s) durability.

We target an availability of 99.99% (4 9\'s) for Convex deployments
although these may experience downtime for maintenance without notice. A
physical outage may affect availability of a deployment but will not
affect durability of the data stored in Convex.

## Limits​

The maximum record size is 1 MB. Convex also limits the size and nesting
depth of the documents stored in the system as described in Field
Values. The maximum number of tables is 10,000. Convex does not enforce
a maximum file size for uploads to File Storage, although upload
attempts will timeout after 2 minutes.

We limit free plans to 1,000,000 records and 500 MB. Free File Storage
is limited to 1 GB of storage and 1 GB/month of serving.

After these limits are hit, new mutations that attempt to commit more
insertions or updates will fail. Paid plans have no hard limits - they
can scale to billions of records and TBs of storage. For more
information see our plans.

## Features​

Convex is under very active development and this section outlines some
areas of currently missing functionality. We\'d love to hear more about
your requirements in the Convex Discord Community.

### Schema enforcement and migrations​

Currently Convex schemas are used to generate TypeScript types but we
don\'t support enforcing the schema at runtime. We plan to add that in
the future along with support for migrating data as your schema changes.

### Input validation​

Currently Convex doesn\'t have a built-in way to validate that the
arguments to Convex functions are the correct types. Even if you use
TypeScript, it is still important for security to check that your inputs
are the correct types at runtime. For more information see the OWASP
Input Validation Cheat Sheet.

You can add input validation to your Convex functions using a third
party library like Zod, Yup, or Superstruct.

### Authorization​

Convex currently has an *authentication framework* which verifies user
identities. In the future we plan to add an *authorization framework*
which will allow developers to define what data a user can access.

For now, you can implement manual authorization checks within your
queries and mutations, but stay tuned for a more comprehensive,
fool-proof solution in the future.

### Telemetry​

Currently, the dashboard provides only basic metrics. Serious sites at
scale are going to need to integrate our logs and metrics into more
fully fledged observability systems that categorize them and empower
things like alerting.

Convex will eventually have methods to publish deployment data in
formats that can be ingested by third parties.

### Analytics / OLAP​

Convex is designed to primarily service all your app\'s realtime
implementation (OLTP) needs. It is less suited to be a good solution for
the kinds of complex queries and huge table scans that are necessary to
address the requirements of analytics (OLAP) use cases.

Convex exposes an Airbyte connector to export Convex data to external
analytics systems.

### Browser support​

Convex does not yet have an official browser support policy, but we
strive to support most modern browsers with significant usage.

### Windows development​

Convex has preliminary support for development on Windows. Some
functionality may be missing or broken. Please report issues at
https://convex.dev/community. If you hit problems, try the Windows
Subsystem for Linux to access the full Convex CLI functionality.

Applications built on Convex will still run on Windows, assuming they
are run in a supported browser.

</div>

</div>

</div>

</div>

</div>
