```js
 1. Error.isError(error); // better error catching
 2. Map.getorInsert(key, value); // if exist - get, if not, insert
 2.1 Map.getOrInsertComputed(key, () => value)
 3. Math.sumPrecise(numbers) // sum of numbers
 4. [Symbol.dispose](){} // can use in class/object & as any instance made with `using` keyword, after completing it the instance will be closed auto
 5. Temporal API // for date,time & durations
 6. Array.fromAsync(iterable) // converts async iterable - into array
 7. RegExp.escape(input.value); // escapes all special charaters from input 
 8. await Promose.try(getUser); // better error handling in 'getUser' func

9. 'Event Bubbling:' e.stopPropagation() // stops an event from bubbling up to parent elements.

10. Select tag option value
    <select onChange={e => setSize(Number(e.target.value))}> 
        <option value="5">5</option>
    </select>
// in select tag option value is always a string. So, if we are storing in a state which expects a number, we need to convert it to a number.

11. Array.from()
- useful when you want to create an array of a specific length and initialize it with values.

// create an array of 10 elements
const arr = Array.from({length: 10}, (_, i) => i + 1);
// if used by `new keyword, indexes won't be initialized`
[...new Array({numberOfItems})].map((_, i) => i + 1)  // good for dynamic items count

- `new Array(10)` creates an array with 10 empty slots.
- `Array.from({length: 10})` creates an array with 10 `undefined` values.


12. import user from "./user.json" with {type:"json"}; 




 ```