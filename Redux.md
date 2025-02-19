## Modern Redux

### Redux Toolkit

1. Install Redux Toolkit and React-Redux
   ```sh
   npm install @reduxjs/toolkit react-redux
   ```
2. Create a Redux Store

   _Create a file named `src/stateManagement/store.js`. Import the configureStore API from Redux Toolkit. We'll start by creating an empty Redux store, and exporting it._

    `stateManagement/store.js`
    ```sh
    import { configureStore } from '@reduxjs/toolkit'

    export default configureStore({
    reducer: {}
    })
    ```
3. Provide the Redux Store to React
    _Once the store is created, we can make it available to our React components by putting a React-Redux `<Provider>` around our application in `src/App.js`. Import the Redux store we just created, put a `<Provider>` around your `<App>`, and pass the store as a prop._

    `App.js`
    ```sh
    import logo from './logo.svg';
    import './App.css';
    import { Provider } from 'react-redux';
    import {store} from './stateManagement/store';
    import Counter from './components/Counter';

    function App() {

    return (
        <div className="App">
            <Provider store={store}>
            <Counter/>
            </Provider>
        </div>
    );
    }

    export default App;
    ```
4. Create a Redux State Slice
    _Add a new file named `src/stateManagement/slice.js`. In that file, import the `createSlice` API from Redux Toolkit._

    `stateManagement/slice.js`
    ```sh
    import { createSlice } from '@reduxjs/toolkit'

    export const counterSlice = createSlice({
    name: 'counter',
    initialState: {
        value: 0
    },
    reducers: {
        increment: (state, action) => {
        return state + 1;
        },
        decrement: (state, action) => {
        return state + 1;
        },
        reset: (state, action) => {
        return state;
        }
    }
    })

    // Action creators are generated for each case reducer function
    export const { increment, decrement, reset } = counterSlice.actions;

    export default counterSlice.reducer;
    ```
5. Add Slice Reducers to the Store
    _Next, we need to import the reducer function from the counter slice and add it to our store. By defining a field inside the `reducer` parameter, we tell the store to use this slice reducer function to handle all updates to that state._

    `stateManagement/store.js`
    ```sh
    import { configureStore } from '@reduxjs/toolkit'
    import counterReducer from '../stateManagement/counterSlice'

    export default configureStore({
    reducer: {
        counter: counterReducer
    }
    })
    ```
6. Use Redux State and Actions in React Components
    _Now we can use the React-Redux hooks to let React components interact with the Redux store. We can read data from the store with useSelector, and dispatch actions using useDispatch. Create a `src/components/Counter.js` file with a `<Counter>` component inside, then import that component into `App.js` and render it inside of `<App>`._

    `components/Counter.js`
    ```sh
    import React from 'react'
    import { useDispatch, useSelector } from 'react-redux';
    import { increment, decrement, reset } from '../stateManagement/slice';

    function Counter () {
        const count = useSelector((state) => state.counter);
        const dispatch = useDispatch();
    return (
        <div>
            <h2>Counter : {count}</h2>
            <button onClick={()=> dispatch(increment())}>increment</button>
            <button onClick={()=> dispatch(decrement())}>decrement</button>
            <button onClick={()=> dispatch(reset())}>reset</button>
        </div>
    )
    }

    export default Counter;
    ```
    _Now, any time you click the "Increment" and "Decrement" buttons:_

    * The corresponding Redux action will be dispatched to the store
    * The counter slice reducer will see the actions and update its state
    * The `<Counter>` component will see the new state value from the store and re-render itself with the new data
