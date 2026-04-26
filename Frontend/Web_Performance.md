## Code-Level Optimizations

Problem: Unpredictable JavaScript Engine Performance
Solution: Write predictable code by defining variables and functions in a structured, consistent manner 

Problem: Expensive String Comparisons
Solution: Use numerical constants instead of string constants to achieve O(1) complexity .

Problem: Object Shape Transitions
Solution: Define object structures consistently upon creation to avoid hidden class transitions that slow down the engine.


### Build-Time Optimizations

Problem: Large Initial Bundle Size
Solution: Implement code splitting and lazy loading for components, pages, and third-party modules to defer loading non-critical code 

Problem: Unnecessary Dependencies
Solution: Use tools like Bundle Phobia or Webpack Bundle Analyzer to audit dependencies and remove unused code via tree shaking.


### Runtime & DOM Optimizations

Problem: Expensive DOM Updates in Loops
Solution: Avoid repeatedly querying or updating the DOM inside loops. Use Document Fragments to batch updates and perform a single injection into the DOM

Problem: Layout Thrashing
Solution: Minimize layout-inducing property changes (e.g., width, height, left, top) in JavaScript. Batch these changes using CSS classes or `requestAnimationFrame` 

Problem: High Latency from External Requests
Solution: Batch HTTP requests and use `requestIdleCallback` for low-priority background tasks to prevent main-thread blockage.

### Deployment & Delivery Optimizations

Problem: Slow Server Responses
Solution: Use CDNs (Content Delivery Networks) to serve content closer to the user and ensure your server supports compression like Brotli 

Problem: Connection Latency
Solution: Utilize resource hints like `preconnect`, `preload`, and `prefetch` to prepare network connections and assets for upcoming user actions.

Problem: Cumulative Layout Shift (CLS)
Solution: Always provide explicit height and width attributes for images and media to prevent layout jumps as content loads.

### Best Practices & Monitoring

Problem: Over-Optimization
Solution: Avoid premature optimization. Only optimize after profiling with tools like Lighthouse or WebPageTest.

Problem: Testing in Ideal Conditions
Solution: Always profile under throttled network and CPU conditions to simulate the experience of real-world users on slower hardware 

### When NOT to prefer optimization:

Before Profiling: Never implement performance fixes without first identifying the specific cause through profiling. 

Applying generic fixes blindly can sometimes make an application slower.

When the impact is negligible: Avoid getting bogged down in minor technical debates (like `var` vs `let`).

Without a clear metric: Don't guess which parts of the app are slow.

 Always use numbers (via tools like Lighthouse or Chrome DevTools) to identify what is actually causing the bottleneck before attempting to "fix" it.

3000 length array is okay without optimization, if code isn't buggy.

- Always add fixed height and width in image, serve images based on device size(picture tag),  aspect ratio,
- In CSS file, never ads classes by HTML tag, use ID or class only
- Schedule low priority task
- Less API calls

# LCP

Causes of Poor LCP:
- Slow server response: Delays in sending HTML (TTFB).
- Render-blocking assets: Heavy CSS or JS files delaying the paint.
- Large, unoptimized media

- Client-side rendering: Relying on the browser to assemble content.
Resource discovery delays: The browser is too busy to find the main content.
Lazy-loading the LCP element: Preventing priority downloading of the hero image.

How to Fix LCP:
Prioritize the LCP element: Use `fetchpriority="high"` for your hero image.
Avoid lazy-loading: Never lazy-load the largest visible element.
Preload critical resources: Help the browser find essential files early.
Inline critical CSS: Include key styles directly in the HTML.
Optimize media: Use efficient formats (WebP/AVIF) and a CDN.
Use SSR: Server-side rendering ensures the page is ready instantly.

Edge Cases:
Early user interaction: If a user scrolls or clicks, the browser stops tracking LCP, which can lead to misleading, "artificially good" performance scores.

# CLS

The 500ms Rule: Any layout shift occurring within 500 milliseconds of a user interaction (click, tap, or key press) is considered "expected" and is excluded from the CLS score.

Session Windows: CLS is calculated in "session windows." Only the worst-performing 5-second window of layout shifts is reported, rather than the sum of every shift on the page.

- Common Causes of Bad CLS
Images or videos without defined height and width attributes.
Dynamically injected content (ads, banners, or pop-ups) added above existing content without reserved space.
Web fonts causing shifts when the fallback font is swapped.
Animating non-transform CSS properties (like top, left, or margin).

How to Fix Bad CLS
- Reserve Space: Always set explicit height and width for media or use the `aspect-ratio` CSS property to prevent content from jumping when elements load.
- Handle Font Swaps: Use CSS `font-display: swap` along with `size-adjust`, `ascent-override`, and `descent-override` to match fallback fonts to the web font size.
- Use Transforms: When animating, use `transform` (e.g., scale or translate) instead of modifying layout-triggering properties like `margin` or `top`.
- SSR: Use Server-Side Rendering to deliver the final HTML layout immediately, reducing the need for async content injection.

Ready-to-Use Code Concepts
Reserve space for images:
`img { width: 100%; height: auto; aspect-ratio: 16/9; }`
CSS Font Adjustment:
`@font-face { font-family: 'Fallback'; size-adjust: 90%; ascent-override: 80%; descent-override: 20%; }`
Loading Placeholders: Always ensure your containers have a minimum height (`min-height`) reserved before async data arrives to prevent the "shift" when the data is finally rendered.


# INP 

INP (Interaction to Next Paint) is a Core Web Vital metric that measures the latency of all user interactions with a page.
- What is INP?
INP is a Core Web Vital that measures a page's overall responsiveness to user interactions. It tracks the time from when a user interacts with a page (e.g., clicks, taps, or key presses) until the next frame is visually updated on the screen. It evaluates the slowest interaction throughout the entire lifecycle of a page.

- How is it Scored?
- Good: Feedback within 200 milliseconds.
- Needs Improvement: 200 to 500 milliseconds.
- Poor: Over 500 milliseconds.
- Note: Interactions like scrolling, hovering, or pinching to zoom do not count toward INP as they are handled by the browser's compositor thread, not the main thread.

- The Three Phases of INP
1. Input Delay: The time between the user's action and when the browser can start processing the event handler (often due to the main thread being busy).
2. Processing Duration: The time taken by the event handlers themselves to execute.
3. Presentation Delay: The time needed for the browser to calculate styles, perform layout, and paint the next frame.

- Common Causes of Poor INP
1. Long-running JavaScript tasks that block the main thread.
2. Heavy or inefficient event handlers.
3. Excessive DOM size.
4. Layout thrashing and third-party script overhead.

- How to Optimize INP
1. Break up long tasks: Use setTimeout or scheduler.yield to return control to the browser.
2. Update UI first: Prioritize critical visual updates and defer non-essential logic.
3. Improve code efficiency: Aggressively split code, reduce DOM complexity, and audit third-party scripts.
4. Use browser tools: Monitor the 'Performance' tab in your browser's Developer Tools to identify slow interactions and bottlenecks.

