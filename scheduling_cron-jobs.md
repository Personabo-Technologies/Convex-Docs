<div>

<div>

<div>

<div>

-   Home
-   Scheduling
-   Cron Jobs

<div>

On this page

</div>

<div>

<div>

# Cron Jobs

</div>

**Example:** Cron Jobs

Convex allows you to schedule functions to run on a recurring basis. For
example, cron jobs can be used to clean up data at a regular interval,
send a reminder email at the same time every month, or schedule a backup
every Saturday.

## Defining your cron jobs​

Cron jobs are defined in a `crons.ts` file in your `convex/` directory
and look like:

<div>

<div>

convex/crons.ts

</div>

<div>

    import { cronJobs } from "./_generated/server";

    const crons = cronJobs();

    crons.interval(
      "clear messages table",
      { minutes: 1 }, // every minute
      "clearAllMessages"
    );

    crons.monthly(
      "payment reminder",
      { day: 1, hourUTC: 16, minuteUTC: 0 }, // Every month on the first day at 8:00am PST
      "actions/sendPaymentEmail",
      { email: "my_email@gmail.com" } // argument to sendPaymentEmail
    );

    // An alternative way to create the same schedule as above with cron syntax
    crons.cron(
      "payment reminder duplicate",
      "0 16 1 * *",
      "actions/sendPaymentEmail",
      { email: "my_email@gmail.com" } // argument to sendPaymentEmail
    );

    export default crons;

<div>

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

</div>

</div>

</div>

The first argument is a unique identifier for the cron job.

The second argument is the schedule at which the function should run,
see Supported schedules below.

The third argument is the name of the public function or internal
function, either a mutation or an action.

## Supported schedules​

-   `interval` runs a function every specified number of `seconds`,
    `minutes`, or `hours`. The first run occurs when the cron job is
    first deployed to Convex. Unlike traditional crons, this option
    allows you to have seconds-level granularity.
-   `cron` the traditional way of specifying cron jobs by a string with
    five fields separated by spaces (e.g. `"* * * * *"`). Times in cron
    syntax are in the UTC timezone. Crontab Guru is a helpful resource
    for understanding and creating schedules in this format.
-   `hourly`, `daily`, `weekly`, `monthly` provide an alternative syntax
    for common cron schedules with explicitly named arguments.

## Viewing your cron jobs​

You can view all your cron jobs in the Convex dashboard cron jobs view.
You can view added, updated, and deleted cron jobs in the logs and
history view. Results of previously executed runs of the cron jobs are
also available in the logs view.

## Error handling​

Mutations and actions have the same guarantees that are described in
Error handling for scheduled functions.

At most one run of each cron job can be executing at any moment. If the
function scheduled by the cron job takes too long to run, following runs
of the cron job may be skipped to avoid execution from falling behind.
Skipping a scheduled run of a cron job due to the previous run still
executing logs a message visible in the logs view of the dashboard.

</div>

</div>

</div>

</div>

</div>
