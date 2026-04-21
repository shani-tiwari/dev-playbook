# React and UI Concepts

## React Hooks and Optimization
- `useMemo`: The value object is recreated on every render, and that can cause all context consumers to re-render even when the actual values have not changed.

```JSX
<AuthContext.Provider
    value={
        useMemo( () => ({ user, setUser, loading, setLoading }), [user, loading] )
    }
>
    {children}
</AuthContext.Provider>
```

## UI and Animation (Framer Motion)
1. `AnimatePresence` + `layout="preserve-aspect-ratio"`: For smooth scaling of text, good for content that changes on some trigger.
    - As a div scales up, the inside text should also scale up with a smooth transition only.
    - Otherwise it gets blurred out or distorted in mid transition.
    - In some cases, adding animation on it or `text-shadow` to make it look crisp will work.

## General JavaScript / UI Tips
- Event Bubbling: `e.stopPropagation()` stops an event from bubbling up to parent elements.

- Digital Clock Setup:
  1. `Date().toLocaleTimeString()`: Gives full time format. Uses a single timezone and doesn't care about other time zones. Can't change format easily and is heavy in call (searches from a large array every time called).
  2. `padStart(2, '0')`: Make string minimum length 2. If not, add '0' at the start. Useful for formatting hours/minutes/seconds.
  3. Inspect tools: 3 dot menu -> more tools -> sensors (can be used to change device location for testing time zones/geolocation).

- Framer (Design Tool):
  1. Vector sets: assets -> vector -> new set of vector assets.
  2. Icons from multiple paths: group them (`ctrl+g`) and tweak properties.
