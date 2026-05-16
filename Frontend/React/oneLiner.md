* requestIdleCallback(callbackFn, options) -- use for low priority task, execute when browser is idle/free. (after paint)

* requestAnimationFrame(callbackFn) - schedule UI work. Browser fires before next repaint, syncing your update with browser's refresh rate. (before paint) - use for animations