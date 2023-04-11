<div>

<div>

<div>

<div>

-   Home
-   Get Started
-   React Native

<div>

<div>

# React Native Quickstart

</div>

Learn how to query data from Convex in a React Native app.

1.  <div>

    <div>

    <div>

    Create a React Native app

    </div>

    Create a React Native app using the `npx create-expo-app` command.

    </div>

    <div>

    <div>

    <div>

        npx create-expo-app my-app

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

    Navigate to your app and install `convex` and its peer dependencies.

    </div>

    <div>

    <div>

    <div>

        cd my-app && npm install convex react-dom react-native-get-random-values

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

    Install .env helper tool

    </div>

    To configure your Convex deployment URL via `.env` files, install
    `react-native-dotenv`.

    </div>

    <div>

    <div>

    <div>

        npm install --dev react-native-dotenv

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

    Configure Babel for .env files

    </div>

    To use the deployment URL directly from the `.env` files, configure
    babel.

    </div>

    <div>

    <div>

    <div>

    babel.config.js

    </div>

    <div>

        presets: ["babel-preset-expo"],
        plugins: ["module:react-native-dotenv"],

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

7.  <div>

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

8.  <div>

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

9.  <div>

    <div>

    <div>

    Connect the app to your backend

    </div>

    In `App.js`, create a `ConvexReactClient` and pass it to a
    `ConvexProvider` wrapping your app.

    Import \'react-native-get-random-values\' as well.

    </div>

    <div>

    <div>

    <div>

    App.js

    </div>

    <div>

        import { ConvexProvider, ConvexReactClient } from "convex/react";
        import 'react-native-get-random-values';
        import { CONVEX_URL } from "@env";

        const convex = new ConvexReactClient(CONVEX_URL, {
          unsavedChangesWarning: false,
        });

        export default function AppWrapper() {
          return (
            <ConvexProvider client={convex}>
              <App />
            </ConvexProvider>
          );
        }

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

10. <div>

    <div>

    <div>

    Display the data in your app

    </div>

    Then in the `App` component use the `useQuery` hook to fetch from
    your `"getTasks"` API.

    </div>

    <div>

    <div>

    <div>

    App.js

    </div>

    <div>

        import { useQuery } from "./convex/_generated/react";

        function App() {
          const tasks = useQuery("getTasks");
          return (
            <View style={styles.container}>
              <Text>{JSON.stringify(tasks, null, 2)}</Text>
            </View>
          );
        }

    <div>

    ![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)![](data:image/svg+xml;base64,PHN2Zz48cGF0aD48L3BhdGg+PC9zdmc+)

    </div>

    </div>

    </div>

    </div>

    </div>

11. <div>

    <div>

    <div>

    Start the app

    </div>

    Start the app, scan the provided QR code with your phone, and see
    the serialized list of tasks in the center of the screen.

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

------------------------------------------------------------------------

Are you trying to build a universal app targeting both browsers and
mobile devices? Use `npm create tamagui` and apply the steps above to
the `apps/expo` directory and the steps in the Next.js Quickstart to the
`apps/next` directory.

</div>

</div>

</div>

</div>

</div>
