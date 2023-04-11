<div>

<div>

<div>

<div>

-   Home
-   Get Started
-   React

<div>

<div>

# React Quickstart

</div>

Learn how to query data from Convex in a React app.

1.  <div>

    <div>

    <div>

    Create a React app

    </div>

    Create a React app using the `create-react-app` command.

    </div>

    <div>

    <div>

    <div>

        npx create-react-app my-app

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

    Install the Convex client and server library

    </div>

    To get started, install the `convex` package which provides a
    convenient interface for working with Convex from a React app.

    Navigate to your app and install `convex`.

    </div>

    <div>

    <div>

    <div>

        cd my-app && npm install convex

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

    src/convex/getTasks.js

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

    Connect the app to your backend

    </div>

    In `index.js`, create a `ConvexReactClient` and pass it to a
    `ConvexProvider` wrapping your app.

    </div>

    <div>

    <div>

    <div>

    src/index.js

    </div>

    <div>

        import { ConvexProvider, ConvexReactClient } from "convex/react";

        const convex = new ConvexReactClient(process.env.REACT_APP_CONVEX_URL);
        root.render(
          <React.StrictMode>
            <ConvexProvider client={convex}>
              <App />
            </ConvexProvider>
          </React.StrictMode>
        );

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

    Display the data in your app

    </div>

    In `App.js`, use the `useQuery` hook to fetch from your `"getTasks"`
    API function.

    </div>

    <div>

    <div>

    <div>

    src/App.js

    </div>

    <div>

        import { useQuery } from "./convex/_generated/react";

        function App() {
          const tasks = useQuery("getTasks");
          return (
            <div className="App">
              {JSON.stringify(tasks, null, 2)}
            </div>
          );
        }

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

9.  <div>

    <div>

    <div>

    Start the app

    </div>

    Start the app, go to http://localhost:3000 in a browser, and see the
    serialized list of tasks at the top of the page.

    </div>

    <div>

    <div>

    <div>

        npm start

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
