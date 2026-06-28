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


- content-visibility: auto; // makes content invisible when scrolled out of view. gives boost to performance. 
- contain: paint; // tells browser to not paint the content of the element if it is not in view. works with scroll-behavior. 

- you can even use it like this: 
- contain: paint layout; // tells browser to not paint and layout the content of the element if it is not in view. gives more boost to performance.

- if you are using contain property, then always set size: none; (so that browser does not reserve space for the element)