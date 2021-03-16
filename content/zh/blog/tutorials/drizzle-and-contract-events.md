---
title: "毛毛雨和合约活动"
date: "2019-04-05"
author: "Amal Sudama"
published: true
---

Drizzle is ideal for synchronizing contract state with a user interface, but as
dapps grow in complexity we foresee growing demand for coordination with
off-chain services.

The code in this section may be small, but it opens up a powerful mechanism to
enable that coordination. Imagine your dapp needs to send a message whenever a
contract event is generated. Lets see how to make this happen.

This tutorial demonstrates how to use Drizzle to subscribe to smart contract
events.

<iframe width="560" height="315" src="https://www.youtube.com/embed/jGIY_l8oWTQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<p class="font-italic text-center">The finished dapp.

We'll use [`react-toastify`](https://github.com/fkhadra/react-toastify) to alert the user whenever a SimpleStorage contract
event is emitted. We have to declare a <ToastContainer /> component and invoke
`toast.success()` when an event is detected. We'll touch `MyComponent` and the
event reducer respectively.

**A Complete example is available at the following [repo](https://github.com/trufflesuite/drizzle-event-demo).**

<div class="alert alert-info">
  Prerequisite: You should be familiar with Truffle, Drizzle, React and Redux. If you need an introduction please consult the following resources:

<br/><br/>

  <ol>
    <li>[Truffle Quickstart](https://truffleframework.com/docs/truffle/quickstart)</li>
    <li>[Getting Started with Drizzle and React](https://www.truffleframework.com/tutorials/getting-started-with-drizzle-and-react)</li>
    <li>[Tutorial: Intro to React](https://reactjs.org/tutorial/tutorial.html)</li>
    <li>[Redux Basic Tutorial](https://redux.js.org/basics/basic-tutorial)</li>
    <li>[Redux Saga](https://redux-saga.js.org/)</li>
    <li>[Redux Middleware](https://redux.js.org/advanced/middleware#middleware)</li>
  </ol>
</div>

# Unbox Drizzle

Let's use `truffle unbox` to bootstrap a project and then wire up a contract
event to a display component by creating a reducer and hook it up to Drizzle's
`EVENT_FIRED` action.

注意: More Drizzle actions are listed in our [Drizzle Actions documentation](/docs/drizzle/reference/drizzle-actions).

First create an empty directory, navigate to it, and `unbox` Drizzle.

```bash
// In the project directory...
$ truffle unbox drizzle
```

Now let's start the `truffle develop` console (which runs a Ganache test blockchain in the background):

```
$ truffle develop
```

Finally, in our Truffle develop console, let's compile and migrate our smart contracts.

```shell
truffle(develop)> compile

# some output here...

truffle(develop)> migrate
```

Now that we have a test chain running and our smart contracts deployed, let's add a toast notification to the UI.

# Listen for Contract Events

We want to listen for the `SimpleStorage` contract's `StorageSet` event and show a toast notification once it fires.

The front end code is located under the `app` folder. Lets add the notification
library `react-toastify` to simulate an external interaction.

```shell
$ cd app
$ npm install react-toastify
```

For the sake of simplicity, we will work in one file, `./app/src/middleware/index.js`.

```shell
$ mkdir ./src/middleware
$ touch ./src/middleware/index.js
```

Import `EventActions` and `generateStore` from Drizzle as well as
toast from `react-toastify`, and `drizzleOptions`.

```javascript
// ./app/middleware/index.js
import { generateStore, EventActions } from "@drizzle/store";
import drizzleOptions from "../drizzleOptions";
import { toast } from "react-toastify";
```

The action `EventActions.EVENT_FIRED` is emitted whenever a contract event is
detected in a Block. We will gain access to it by registering a custom
middleware with the Redux store. As you know, Redux middleware comprises a set
of functions executed in a sequence that processes each dispatched actions
before passing them to Reducers.

```javascript
const contractEventNotifier = (store) => (next) => (action) => {
  if (action.type === EventActions.EVENT_FIRED) {
    const contract = action.name;
    const contractEvent = action.event.event;
    const message = action.event.returnValues._message;
    const display = `${contract}(${contractEvent}): ${message}`;

    toast.success(display, { position: toast.POSITION.TOP_RIGHT });
  }
  return next(action);
};
```

Now lets register this middleware with Drizzle. `generateStore` will return a
Redux store that you can use anywhere you can use a store. We will export it to
be used by `DrizzleProvider`.

```javascript
const appMiddlewares = [contractEventNotifier];

export default generateStore({
  drizzleOptions,
  appMiddlewares,
  disableReduxDevTools: false, // enable ReduxDevTools!
});
```

## Connect the Store

Send the `store` as a prop to `DrizzleProvider`

```javascript
// App.js
...
import store from './middleware'
...
<DrizzleProvider store={store} options={drizzleOptions}>
...
```

## Hook up Display

Modify `MyComponent.js` to import `ReactToastify.css` and configure `ToastContainer`

```javascript
...
import { ToastContainer } from 'react-toastify'
import 'react-toastify/dist/ReactToastify.css'
...

export default ({ accounts }) => (
  <div className="App">
    <ToastContainer />
  ...
  </div>
```

## A Quick Test

- Things often go south during development so a pretest check is in order.

  1. MetaMask should NOT be on Main net! Do not run this if you're on main
     net!
  1. Is MetaMask listening on the correct port defined above? Metamask should
     have ETH funds. Something is amiss if it doesn't.
  1. Are the smart contracts deployed from the correct directory?

- Fire up the app.
  ```shell
  $ npm run start
  ```
- Change SimpleStorage's `stored Value`
  ![Change SimpleStorage value!](/img/tutorials/drizzle-and-contract-events/stored-value.gif)

- You'll be rewarded with a toast notification when the transaction is completed.
  ![Toast](/img/tutorials/drizzle-and-contract-events/alert-toast.png "A
successful Toast!")

The dapp is now a consumer of Drizzle's `EVENT_FIRED` action item and can
coordinate with other services to implement its business logic.

More Drizzle actions are listed in our [Drizzle Actions documentation](/docs/drizzle/reference/drizzle-actions).
