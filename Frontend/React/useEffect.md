# useEffect
- runs after paint, by the time your effect runs, user has already seen the previous frame.
- React calls it in one of them (setTimeout, requestAnimationFrame, requestIdleCallback)
- use when u don't have to show any feedback to user on state change 

## Bugs: 
* UI Flickering - User clicks the filter button. The UI immediately resets to the default (e.g., "No data") while the new data is still loading in the background.
    Once the data arrives, the UI updates again. This rapid flash from Old UI → Empty UI → New UI is visually jarring. 
    -- to fix this we can use skeleton loader
    -- if a value can be derived from props or state, derive it, don't store it.
            
* Empty State Flash - User opens the dashboard. Sees 'No data yet' for half a second, then list appears(API call in useEffect)
    -- Optional chaining
    -- skeleton loader or place placeholder (as api call will happen after first paint/render)
    -- use React Query, Tanstack Query
    -- use suspense and for data fetch use "use" by react
    
    
* Subscription Delays - External Store Updates (* useSyncExternalStore - read the store synchronously & concurrent-safe by design)
Component renders with the state value, Re-renders again with the right one.


# Use it for:
- Local State, props, redux state change
- side effects that must run after a commit(logging, anakytics)
- when the change come from many sources, not a single event 


# Don't use it for:
- External stores, browser APIs - use useSyncExternalStore
- expensive calculations - use useMemo, useTrasferable
- deriving state from props or other state - do it in/during render
- responding to an user event - put it in event handler



* Use - useLayoutEffect() for above bugs
- but, it blocks paint(runs before paint synchronously), so use only when necessary 
- DOM related work - use useLayoutEffect(), measure something and update state (DOM related work)
- want to read value