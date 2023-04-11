<div>

<div>

<div>

<div>

-   Home
-   Database
-   Import & Export
-   Snapshots

<div>

On this page

</div>

<div>

<div>

# Exporting Data Snapshots

</div>

You can export your data from Convex using Snapshot export, which you
can find in the settings page of your project in the dashboard.

When you request an export, Convex will generate a JSON file for each
Convex table in your deployment with the latest version of every
document at the time of your request. This may take a few seconds or a
few minutes, depending on how much data is in your deployment. You can
download the files by clicking on the links in the Latest Snapshot
table. Each export is a consistent snapshot of your data at the time of
your request, and each JSON is an array of documents from a single
table, ordered by `_id`.

## FAQ​

### Can I use snapshot export as a backup?​

Right now, you can only access one export at a time, so this is not an
automated backup system. You are welcome to download your tables
routinely, and feel free to chime in on Discord if you would like to see
better support for backups.

### Are there any limitations?​

Snapshot export is only available for deployments with less than 128
tables. Each export is accessible for up to 14 days (if no more exports
are requested). There is no limit to how many exports you can request.

</div>

</div>

</div>

</div>

</div>
