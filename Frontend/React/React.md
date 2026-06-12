# React and UI Concepts

## React Hooks and Optimization

### `useMemo`: The value object is recreated on every render, and that can cause all context consumers to re-render even when the actual values have not changed.

```JSX
<AuthContext.Provider
    value={
        useMemo( () => ({ user, setUser, loading, setLoading }), [user, loading] )
    }
>
    {children}
</AuthContext.Provider>
```



- Digital Clock Setup:
  1. `Date().toLocaleTimeString()`: Gives full time format. Uses a single timezone and doesn't care about other time zones. Can't change format easily and is heavy in call (searches from a large array every time called).
  2. `padStart(2, '0')`: Make string minimum length 2. If not, add '0' at the start. Useful for formatting hours/minutes/seconds.
  3. Inspect tools: 3 dot menu -> more tools -> sensors (can be used to change device location for testing time zones/geolocation).



## React parent-child/child-parent communication
- parent-child: passing data from parent to child is easy, just pass props to child.
- child-parent: passing data from child to parent is not straightforward. Child component can not directly update parent state.
    - Child component can call a function passed as a prop from parent to update the parent state.
    - for e.g. input form in child component can call a function passed as a prop from parent to update the parent state.
    - example : 

    ```jsx
    function Parent() {
        const [message, setMessage] = useState('');
        return (
            <div>
                <Child onMessageChange={setMessage} />  // passing the setMessage function as a prop to child
                <p>Received: {message}</p>
            </div>
        );
    }

    function Child({ onMessageChange }) {  // got the function from parent as a prop
        return (
            <input
                type="text"
                onChange={e => {
                    onMessageChange(e.target.value); // call parent's function and pass the value
                }}
            />
        );
    }
    ```
    - In this example, when user types in the input field in `Child` component, it calls the `onMessageChange` function passed as a prop from `Parent` component. This function updates the `message` state in `Parent` component, which in turn re-renders `Parent` component and displays the updated message.    





# stnc/async problen
- A function that have some sync/async code, and error in sync part of code.
- Calling it by `await` and that error didn't caught, even if we called it inside `try/catch` 
- so we should call it like 
```js
await Promose.try(getUser); //remove try/catch now
```



# convert iterable into an array
- Async Generator function 
```js 
async function* asyncGenerator() {
  await Promise.resolve(1);
  yield 2;
  yield 3;
}
const asyncIterator = asyncGenerator();
```
- use `Array.fromAsync` to convert async iterable into array
```js
const result = await Array.fromAsync(asyncIterator);
console.log(result); // [1, 2, 3]
```

# Error check
```js
if(e instanceof Error)  // check relies on object identity (works in same realm, e.g. iframe vs parent iframe)
if(Error.isError(error)) // proper realm-agnostic error check (all realm)
```


