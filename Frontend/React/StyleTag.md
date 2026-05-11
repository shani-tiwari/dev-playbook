* you can add style tag right into your jsx like this --

```jsx
<style jsx>{`
    /* your css styles here */
`}</style>
```

- use this when you want to add style for specific component only.
- or an animation, that you want to bundle with the component.

- you can also add global css in that file by targeting `document` -- 

```jsx
<style jsx>{`
    @import "tailwindcss";

    /* Your styles */
`}</style>
```