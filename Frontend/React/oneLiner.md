
* requestIdleCallback(callbackFn, options) -- use for low priority task, execute when browser is idle/free. (after paint)

* requestAnimationFrame(callbackFn) - schedule UI work. Browser fires before next repaint, syncing your update with browser's refresh rate. (before paint) - use for animations

* User agent shadow dom - option in inspect setting let's you see the default styling of any element browsers does for them by their own. 
  - those are called 'shadow-dom' components.
  - and we can override it too - using ::-webkit-progress-bar, ::-webkit-progress-bar etc 