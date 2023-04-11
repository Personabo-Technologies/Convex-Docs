<div>

<div>

<div>

<div>

-   Home
-   Database
-   Import & Export
-   Streaming

<div>

On this page

</div>

<div>

<div>

# Using Convex with Airbyte

</div>

Airbyte is a data-integration platform that allows you to sync your
Convex data into other databases. This can be useful for handling
queries and workloads that aren\'t supported by Convex directly. Some
example use cases include:

1.  Analytics
    -   Convex isn\'t optimized for queries that load huge amounts of
        data. A data platform like Databricks or Snowflake is more
        appropriate.
2.  Search
    -   Convex doesn\'t currently efficiently support queries that look
        for substrings in text fields. Databases like ElasticSearch are
        designed for these queries.
3.  Machine Learning training
    -   Convex isn\'t optimized for queries running computationally
        intensive machine learning algorithms.

Using Airbyte allows you to replicate individual Convex tables into any
of their supported destinations.

## Connecting to Airbyte​

If you haven\'t done so, sign up for Convex Professional to enable
Airbyte support for your Convex team.

If you haven\'t done so, get started with Airbyte. You can use Airbyte
Open Source free.

1.  Within Airbyte, create a new Source. Select \"Convex\" from the
    dropdown.
2.  In another tab, go to the Convex Dashboard.
3.  Select your project and ensure you have selected the Production
    deployment.
4.  Click the \"Settings\" button on the left-hand side of the page, and
    generate a \"Deploy key\".
5.  Back in the Airbyte tab, paste the deploy key as \"Access Key\".
6.  Back in the Convex dashboard Settings page, copy the \"Deployment
    URL\".
7.  Back in the Airbyte tab, paste the deployment URL.
8.  Click \"Set up source\".

Now you have connected Convex to Airbyte! Follow prompts to connect
Airbyte to a data destination, such as Databricks or Elasticsearch.

Choose a replication frequency, which is how often data will be synced
out of Convex and into the destination.

Choose the Convex tables to sync over, and how it should be synced.
Airbyte has several sync modes. Convex supports all of them and
recommends \"Incremental + Deduped History\" to reduce sync times and
make the destination reflect document edits and deletes.

Click \"Set up connection\" to start syncing. Once the data has synced,
you can query your Convex data within the destination.

</div>

</div>

</div>

</div>

</div>
