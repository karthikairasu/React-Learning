## 1. React Virtual Dom
        The Virtual DOM is a lightweight in-memory representation of the actual DOM, When something in the app changes (like a user clicks a button or data updates), the changes are first applied to this virtual version instead of the real DOM.

    ### 🔧 How It Works

    #### 1. Initial Render
    - React builds a virtual DOM tree that mirrors the structure of the real DOM.

    #### 2. State/Props Change
    - When a component's **state** or **props** change, React:
    - Creates a new Virtual DOM based on the updated data.
    - Compares (diffs) the new Virtual DOM with the previous one.

    ---

    ### ⚙️ Diffing Algorithm

    - React uses a fast reconciliation process to detect what has changed in the virtual DOM.
    - The algorithm quickly identifies differences between the old and new virtual DOMs.

    ---

    ### 🚀 Efficient Updates

    - Only the changed elements are updated in the real DOM.
    - This reduces expensive DOM operations and boosts performance.

## 2. Pure Component
   
    - In React, a Pure Component is a type of component that implements a shallow comparison on its props and state to decide whether it should re-render. This optimization can help improve performance by preventing unnecessary renders
    - Shallow Comparison

## 3. Life Cycle Function Component

    1. Mounting Phase (👇 Equivalent of componentDidMount) 
   
       - The empty dependency array [] means this effect runs only once, after the first render.
        
        useEffect(() => {
            console.log("Component mounted");

            // This runs once when the component is first rendered

        }, []);

    2. Updating Phase (👇 Equivalent of componentDidUpdate) 
   
        - This effect runs whenever count changes.

        useEffect(() => {
            console.log("Count updated:", count);
        }, [count]);

    3. Unmounting Phase (👇 Equivalent of componentWillUnmount)

        - return function useEffect inside [] array cleanup before unmount.
        - The cleanup function (the return) runs only once, right before the component unmounts (just like componentWillUnmount).
  
        useEffect(() => {
            // setup
            console.log("Component mounted");

            return () => {
                // cleanup
                console.log("Component will unmount");
            };
        }, []);

## 4. Higher Order Component
        - An HOC is a function that takes a component as an argument and returns a new component with enhanced functionality. HOCs do not modify the original component passed into them. Instead, they create a new component by wrapping the original component within it. 