<div>

<div>

<div>

<div>

-   Home
-   Tools
-   Convex CLI

<div>

On this page

</div>

<div>

<div>

# Convex CLI

</div>

The Convex command-line interface (CLI) is your interface for managing
Convex projects and Convex functions.

To install the CLI, run:

<div>

<div>

    npm install convex

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

You can view the full list of commands with:

<div>

<div>

    npx convex -h

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

## Manage Projects​

All of these commands require logging in first with:

<div>

<div>

    npx convex login

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

### Create a new project​

<div>

<div>

    npx convex init

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Create a new Convex project. This command creates:

1.  The `convex/` directory: This is the home for your query and
    mutation functions.
2.  `convex.json`: This is the main configuration for your Convex
    project. It includes a randomly assigned URL for the project in
    production.

### Recreate project configuration​

<div>

<div>

    npx convex reinit

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Recreate `convex.json` if you lose it.

## Write Code​

### Run the Convex dev server​

<div>

<div>

    npx convex dev

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Watch the local filesystem. When your Convex functions change, push them
to your dev deployment and update generated code.

### Deploy Convex functions to production​

<div>

<div>

    npx convex deploy

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

This command will:

1.  Typecheck your Convex functions.
2.  Regenerate the generated code in the `convex/_generated` directory.
3.  Bundle your Convex functions and their dependencies.
4.  Push your functions and indexes to production.

Once this command succeeds the new functions will be available
immediately.

### Update generated code​

<div>

<div>

    npx convex codegen

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Update the generated code in `convex/_generated` without pushing. This
is useful after adding or removing Convex functions or making schema
changes.

### Typecheck functions​

<div>

<div>

    npx convex typecheck

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Run TypeScript over all of your functions without pushing.

### Modify authentication settings​

<div>

<div>

    npx convex auth <subcommand>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Update the authentication settings for your application. The possible
subcommands are:

-   `add`
-   `remove`
-   `list`

To learn more about adding authentication to your app, see the
Authentication.

## Misc​

### Open the dashboard​

<div>

<div>

    npx convex dashboard

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Open the Convex dashboard.

### Open the docs​

<div>

<div>

    npx convex docs

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Open these docs!

### Import a file into Convex​

<div>

<div>

    npx convex import <tableName> <path>

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

Import a CSV, JSON, or JSONLines file into a Convex table.

-   CSV files must have a header, and each row\'s entries are
    interpreted either as a (floating point) number or a string.
-   JSON files must be an array of JSON objects.
-   JSONLines files must have a JSON object per line.

The default is to import into your dev deployment. Use `--prod` to
import into your project in production. Imports into a table with
existing data will fail by default, but you can specify `--append` to
append the imported rows to the table or `--replace` to replace existing
data in the table with your import.

#### Limitations​

Currently Convex only supports imports of up to 8192 rows and 8MiB in
size. To work around this, you can split your large import file into
smaller files and run `npx convex import --append` for each one. Feel
free to ping us in the community Discord if you would like better
support for large imports!

</div>

</div>

</div>

</div>

</div>
