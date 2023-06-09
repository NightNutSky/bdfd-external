# Introduction Note

The package was mainly created for better implementation of some features in my [VS Code extension](https://marketplace.visualstudio.com/items?itemName=NightNutSky.bdfd-bds) and for powering my future REST API which will let you access below listed features by making HTTP Requests.

The information about how to get your auth token you can find in [This article](https://github.com/NightNutSky/bdfd-bds/blob/master/Sync%20Resources/SYNC.md#get-the-token) of the Sync guide made for my VS Code Extension.

## BDFD External

BDFD External is a package for parsing BDFD Web App and make requests to it.
Get your bot list and Get, Update, Create & Delete commands and variables externally!

```sh
npm i @nightnutsky/bdfd-external
```
```sh
pnpm add @nightnutsky/bdfd-external
```

## Brief Examples

### Example #1

```ts
import { Bot } from "@nightnutsky/bdfd-external";

const authToken = ''; // Your auth token

Bot.list({ authToken })
.then((list) => {
    const formattedList = list.map((bot) => {
        const {
            botID,
            botName,
            hostingTime
        } = bot;

        return `Bot ${botID}: ${botName}'s hosting time end date: ${hostingTime}`;
    }).join('\n');

    console.log(formattedList);
})
.catch((error) => {
    console.error('An error occured while getting the bot list:', error);
});

```

### Example #2

```ts
import { Variable } from "@nightnutsky/bdfd-external";

const authToken = ''; // Your auth token
const botID = ''; // Your BDFD bot ID

Variable.list({ authToken, botID })
.then((list) => {
    const [variable] = list; // take the first variable
    const {
        variableName,
        variableValue
    } = variable;

    console.log(`The "${variableName || 'Unnamed variable'}" variable's value is "${variableValue || 'Empty'}"`);
})
.catch((error) => {
    console.error('An error occured while getting the variable list:', error);
});
```