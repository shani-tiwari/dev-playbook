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
