# text-box: trim-both cap alphabatic;
- let's u remove the space above & beyond the text.

------

# overscroll-contain (in overlay)
- u have overlay scrollable modal & as u scroll in it your page scrolls with it too(scroll chaining)

------

# corner-shape
- make custom shapes for elements.
- shorthand property - corner-shape-top-left/right, corner-shape-bottom-left/right
```css
.box {
  corner-shape: bevel/scoop/square/round/...;
}
```

------

# dark mode box shadows
- use a layered dark color for the shadow instead of white to add elevation to your cards
```css
box-shadow: rgba(0, 0, 0, 0.42) 0px 54px 55px, rgba(0, 0, 0, 0.36) 0px -12px 30px, rgba(0, 0, 0, 0.20) 0px 4px 6px, rgba(0, 0, 0, 0.10) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
```

------

# snap scroll 
- u have long content and u want to stop at certain elements on scroll.
- parent: snap-x/y snap-mandatory/sn
- child: snap-start/center/end/proportional/inherit