
* requestIdleCallback(callbackFn, options) -- use for low priority task, execute when browser is idle/free. (after paint)

* requestAnimationFrame(callbackFn) - schedule UI work. Browser fires before next repaint, syncing your update with browser's refresh rate. (before paint) - use for animations

* User agent shadow dom - option in inspect setting let's you see the default styling of any element browsers does for them by their own. 
  - those are called 'shadow-dom' components.
  - and we can override it too - using ::-webkit-progress-bar, ::-webkit-progress-bar etc 

* Component vs hooks: - Component should always return something either jsx/null/empty fragment, no need for hooks.

* dynamic object syntax: 
  - ```js 
      const players = { A: 0, B: 1 }; 
      [players.A]: '✖️' -- computed property name
    ```
  
* Array.from() -- requires by which you want to make an array -- or what should be inside the array
  ```js 
    const buttons = Array.from(new Array(9));
  ```

* Deep Clone: Storing player's turns using structured clone otherwise when we modift playerTurn, defaultTurn will also change (due to call by reference)
  ```js 
    const [playerTurn, setPlayerTurn] = useState(structuredClone(defaultTurns));
  ```

* Currying - to return a function, runs on only click event, coz we called it directly at map() earlier 
  ```js
    onClick={handleTurn(i)}
  ```



* “Only call Hooks at the top level.”
  - ✅ Call hooks before conditions
  - ✅ Call hooks before loops
  - ✅ Call hooks before nested functions
  - ❌ Never call hooks inside if, for, while, etc.
```js (wrong implementation)
if (showDetails) {
  const [bio] = useState('React developer from NYC');
  const [joined] = useState('January 2025');
}
```