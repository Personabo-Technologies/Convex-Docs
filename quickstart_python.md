<div>

<div>

<div>

<div>

-   Home
-   Get Started
-   Python

<div>

<div>

# Python Quickstart

</div>

Learn how to query data from Convex in a Python app.

1.  <div>

    <div>

    <div>

    Create a Python script folder

    </div>

    Create a folder for your Python script with a virtual environment.

    </div>

    <div>

    <div>

    <div>

        python3 -m venv my-app/venv

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

2.  <div>

    <div>

    <div>

    Install the Convex client and server libraries

    </div>

    To get started, install the `convex` npm package which enables you
    to write your backend.

    And also install the `convex` Python client library and
    `python-dotenv` for working with `.env` files.

    </div>

    <div>

    <div>

    <div>

        cd my-app && npm install convex && venv/bin/pip install convex python-dotenv

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

3.  <div>

    <div>

    <div>

    Setup a Convex dev deployment

    </div>

    Next, run `npx convex dev`. This will prompt you to log in with
    GitHub, create a project, and save your production and deployment
    URLs.

    It will also create a `convex/` folder for you to write your backend
    API functions in. The `dev` command will then continue running to
    sync your functions with your dev deployment in the cloud.

    </div>

    <div>

    <div>

    <div>

        npx convex dev

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

4.  <div>

    <div>

    <div>

    Create sample data for your database

    </div>

    In a new terminal window, create a `sampleData.jsonl` file with some
    sample data.

    </div>

    <div>

    <div>

    <div>

    sampleData.jsonl

    </div>

    <div>

        {"text": "Buy groceries", "isCompleted": true}
        {"text": "Go for a swim", "isCompleted": true}
        {"text": "Integrate Convex", "isCompleted": false}

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

5.  <div>

    <div>

    <div>

    Add the sample data to your database

    </div>

    Now that your project is ready, add a `tasks` table with the sample
    data into your Convex database with the `import` command.

    </div>

    <div>

    <div>

    <div>

        npx convex import tasks sampleData.jsonl

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

6.  <div>

    <div>

    <div>

    Expose a database query

    </div>

    Add a new file `getTasks.js` in the `convex/` folder with a query
    function that loads the data.

    The default export declares an API function named after the file,
    `"getTasks"`.

    </div>

    <div>

    <div>

    <div>

    convex/getTasks.js

    </div>

    <div>

        import { query } from "./_generated/server";

        export default query(async ({ db }) => {
          return await db.query("tasks").collect();
        });

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

7.  <div>

    <div>

    <div>

    Create a script to load data from Convex

    </div>

    In a new file `main.py`, create a `ConvexClient` and use it to fetch
    from your `"getTasks"` API.

    </div>

    <div>

    <div>

    <div>

    main.py

    </div>

    <div>

        from dotenv import load_dotenv
        load_dotenv('.env.local'); load_dotenv()

        import os
        from convex import ConvexClient
        client = ConvexClient(os.getenv('CONVEX_URL'))
        print(client.query("getTasks"))

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

8.  <div>

    <div>

    <div>

    Run the script

    </div>

    Run the script and see the serialized list of tasks.

    </div>

    <div>

    <div>

    <div>

        venv/bin/python -m main

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

</div>

</div>
