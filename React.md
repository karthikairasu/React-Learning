## Basic Idea of the DOM First - DOM
   Before jumping to Virtual DOM, we need to understand the real DOM:

   - DOM stands for Document Object Model.

   - It’s how your browser represents the structure of an HTML page.

   - It’s tree-like — everything `(like <div>, <p>, etc.)` is a node.

## 1. React Virtual Dom
    
   - The Virtual DOM is a lightweight in-memory (a JavaScript object) representation of the real DOM.
    
   - When the app’s state changes, React creates a new virtual DOM tree and compares it with the previous one using a diffing algorithm, finds the minimal changes, and then updates only those parts in the real DOM.
 
   - This reduces expensive DOM operations and boosts performance. 
    
   - React keeps only one Virtual DOM tree for the whole app at any time. After updating the real DOM, React replaces the old Virtual DOM tree with the new one.

## 2. Pure Component
   
   - In React, a Pure Component is a type of component that implements a shallow comparison on its props and state to decide whether it should re-render. This optimization can help improve performance by preventing unnecessary renders.
    
   - Shallow Comparison

## 3. Life Cycle Function Component

1. Mounting Phase (👇 Equivalent of componentDidMount) 
   
    The empty dependency array [] means this effect runs only once, after the first render.
    ```jsx
    useEffect(() => {
        console.log("Component mounted");

        // This runs once when the component is first rendered

    }, []);
    ```
2. Updating Phase (👇 Equivalent of componentDidUpdate) 
   
    This effect runs whenever count changes.
    ```jsx 
    useEffect(() => {
        console.log("Count updated:", count);
    }, [count]);
    ```
3. Unmounting Phase (👇 Equivalent of componentWillUnmount)

    Return function useEffect inside [] array cleanup before unmount.

    The cleanup function (the return) runs only once, right before the component unmounts (just like componentWillUnmount).
    ```jsx
    useEffect(() => {
        // setup
        console.log("Component mounted");

        return () => {
            // cleanup
            console.log("Component will unmount");
        };
    }, []);
    ```
4. Clean Up Resources on Unmount
     
    When your component is removed, you should clean up things like:

    - Subscriptions
    - Timers/Intervals
    - Event listeners
    - WebSocket connections
  
## 4. What is JSX?

   JSX - JavaScript XML

   - JSX is a syntax extension for JavaScript that allows developers to write HTML-like elements in their JavaScript code.
   - It is used in React to describe the structure and content of a component.
   - JSX is transpiled to plain JavaScript before being executed, so it is compatible with all web browsers.

## 5. React Fragments ?

   - Fragments let you group a list of children without adding extra nodes to the DOM.
   - React Fragments are useful when returning multiple elements from a component without adding extra `<div>` or other wrapper nodes to the DOM.
   ```jsx
        Ex1: return(
                <React.Fragment key={item.id}>...</React.Fragment> //Explicit syntax
            )
        
        Ex2: return(
                <>...</> //Shorthand syntax
            )
   ``` 
 
## 6. Higher Order Component

   - An HOC is a function that takes a component as an argument and returns a new component with enhanced functionality. HOCs do not modify the original component passed into them. Instead, they create a new component by wrapping the original component within it.
       
## 7. Data passing function component 

1. Props (Parent ➝ Child) 
    ```jsx
    function Parent() {
        return <Child name="Karthi" />;
    }

    function Child({ name }) {
        return <p>Hello, {name}</p>;
    }
    ```
2. Callback Functions (Child ➝ Parent)
     - Child sends data back by calling a function received from the parent.
     ```jsx
     function Parent() {
         const handleChildData = (data) => {
             console.log(data);
         };

         return <Child onSend={handleChildData} />;
     }

     function Child({ onSend }) {
         return <button onClick={() => onSend('Hello from Child')}>Send</button>;
     }
     ```
3. React Context API (Global State)
    - For passing data across multiple levels without prop drilling.
     
    ### Create Context
    ` const UserContext = React.createContext(); `
    ### Provider (Top Level)
    ```jsx
    function Parent() {
        return (
            <UserContext.Provider value="Karthi">
            <Child />
            </UserContext.Provider>
        );
    }
    ```
    ### Consumer (Any Level)
    ```jsx
    function Child() {
        const name = React.useContext(UserContext);
        return <p>Hello, {name}</p>;
    }
    ```
## 8. UseEffect?

    useEffect is a React Hook used to handle side effects in functional components, like data fetching, subscriptions, or manually changing the DOM. It runs after the component renders. It mimics lifecycle methods—like componentDidMount, componentDidUpdate, and componentWillUnmount. I used it to fetch user data from an API when the component loads and update the state. I added a dependency array so it only runs when specific props or state change