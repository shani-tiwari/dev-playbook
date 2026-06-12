
* when width changes dynamically, browser will re-calculate the layout of whole page.
 -  which may create an overhead 
 - so, don't use 'width' for animation, use 'transform' or 'animation' property instead.
 - UI paints can be checked in network tab


## UI and Animation (Framer Motion)
1. `AnimatePresence` + `layout="preserve-aspect-ratio"`: For smooth scaling of text, good for content that changes on some trigger.
    - As a div scales up, the inside text should also scale up with a smooth transition only.
    - Otherwise it gets blurred out or distorted in mid transition.
    - In some cases `text-shadow` to make it look crisp, will work.
