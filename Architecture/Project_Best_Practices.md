# WebTree - Best Practices & Functionality Guide

This document outlines the core logic and functional best practices implemented across the WebTree repository. It aims to explain **how** features are implemented and **why** particular patterns are chosen, supplemented by code snippets for context.

---

## 1. Performance & Code Splitting
**How:** We use React's `lazy` and `Suspense` for asynchronous component loading, specifically for heavy or secondary routes like `Collection`.
**Why:** Code splitting reduces the initial JavaScript bundle sent to the client. This results in faster page load times (TTFB) and improved Core Web Vitals, parsing only the code needed for the immediate view.

```javascript
/* src/App.jsx */
import React from "react";
import { Routes, Route } from "react-router";

// Lazy loading the Collection page components
const Collection = React.lazy(() => import("./pages/Collection"));

function App() {
  return (
    <React.Suspense fallback={<div className="text-white text-center p-10">Loading...</div>}>
      <Routes>
        <Route path="/collection" element={<Collection />} />
        {/* other routes */}
      </Routes>
    </React.Suspense>
  );
}
```

---

## 2. Global State Management (Context API & LocalStorage)
**How:** We use React Context (`CollectionContext`, `ReviewContext`) paired with browser `localStorage` to manage global state across the app.
**Why:** For non-critical, user-centric data like saved collections or reviews, we avoid fetching from a backend on every load. This ensures persistence across sessions without the cost of complex state management libraries (like Redux) since the data is relatively small and isolated.

```javascript
/* src/context/CollectionContext.jsx */
export function CollectionProvider({ children }) {
  // Initialize state directly from LocalStorage to avoid content flashes
  const [collection, setCollection] = useState(() => {
    const saved = localStorage.getItem("personalCollection");
    return saved ? JSON.parse(saved) : [];
  });

  // Sync state changes back to LocalStorage securely
  useEffect(() => {
    localStorage.setItem("personalCollection", JSON.stringify(collection));
  }, [collection]);
  
  // Provide values via context
  // ...
}
```

---

## 3. Web Accessibility (A11y)
**How:** WebTree embeds accessibility directly into UI components, including:
- "Skip to main content" links for keyboard navigation.
- Disabling background scroll behaviors when modals/mobile menus are open.
- Using ARIA attributes like `aria-label`, `aria-expanded`, and `aria-live`.

**Why:** It ensures screen readers and keyboard users can navigate freely. Disabling body scroll on open modals prevents "scroll-bleed", a common UX annoyance where the background scrolls invisibly underneath a fixed overlay.

```javascript
/* src/components/Navbar.jsx */
// Lock body scroll when mobile menu is open
useEffect(() => {
  if (isOpen) {
    document.body.style.overflow = "hidden";
  } else {
    document.body.style.overflow = "";
  }
  return () => {
    document.body.style.overflow = "";
  };
}, [isOpen]);

/* Screen reader explicit updates (from Home.jsx) */
<div className="sr-only" aria-live="polite" role="status">
  {activeCategory ? `Showing ${activeCategory.split("_").join(" ")} resources` : ""}
</div>
```

---

## 4. ClassName Merging & Styling
**How:** Utilizing a custom utility function `cn()` built on `clsx` and `tailwind-merge`.
**Why:** React component styling with Tailwind often involves conditionally applying classes based on state or props. Native template literals can lead to specificity conflicts where generic classes might override explicit ones. `cn()` elegantly merges conditional arrays of classes and intelligently resolves Tailwind conflicts.

```javascript
/* src/components/Navbar.jsx */
import { cn } from "../lib/utils";

<Link
  to="/about"
  className={cn(
    // Base styles
    "text-neutral-400 font-mono text-lg transition-all duration-300",
    
    // Conditionally applied active state
    active === "about" && "text-amber-500 underline underline-offset-8"
  )}
>
  About
</Link>
```

---

## 5. UI Animations & Orchestration
**How:** We rely on `framer-motion` (specifically `motion/react`) for layout transition animations, orchestrating entrance animations (like pop-ups), and micro-interactions.
**Why:** Framer Motion integrates beautifully with React's component lifecycle via tools like `AnimatePresence`. It provides physics-based fluid motions (as opposed to rigid keyframes), ensuring that items smoothly flow when a user filters elements or navigates across pages.

```javascript
/* src/pages/Home.jsx - Animating a layout grid when lists change */
import { motion, AnimatePresence } from "motion/react";

<motion.section layout className="grid md:grid-cols-4">
  <AnimatePresence mode="popLayout">
    {data.map((item) => (
      <motion.div
        key={item.id}
        layout
        initial={{ opacity: 0, scale: 0.9 }}
        animate={{ opacity: 1, scale: 1 }}
        exit={{ opacity: 0, scale: 0.9 }}
        transition={{ duration: 0.3 }}
      >
        <Card {...item} />
      </motion.div>
    ))}
  </AnimatePresence>
</motion.section>
```

---

## 6. Comprehensive SEO & Meta Configuration
**How:** WebTree includes extensive `<head>` customizations in `index.html`, including Primary Meta tags, Open Graph (Facebook), Twitter Cards, and Structured Data (JSON-LD).
**Why:** Proper static integration of these values allows web crawlers, search engines, and social media platforms to beautifully render link previews when users share our site. JSON-LD explicitly dictates to Google how to catalog our content contextually.

```html
<!-- index.html -->

<!-- Open Graph / Facebook -->
<meta property="og:type" content="website" />
<meta property="og:url" content="https://webtree.shaniweb.com/" />
<meta property="og:title" content="WebTree | High-Quality Development Resources" />
<meta property="og:image" content="/og-image.png" />

<!-- Structured Data (JSON-LD) -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "WebTree",
  "url": "https://webtree.shaniweb.com/",
  "description": "Curated development resources."
}
</script>
```

---

## 7. Efficient Data Fetching & Placeholder Views
**How:** Fetching JSON data intelligently via native `fetch` over environment endpoints, paired with Skeleton loader displays on loading state.
**Why:** It explicitly ties data to `useEffect` bounds keeping UI logic separate from external effects. Skeletons provide immediate perceptive feedback, making the app feel instantaneously responsive while waiting for the payload.

```javascript
/* src/pages/Home.jsx */
const [data, setData] = useState([]);
const [loading, setLoading] = useState(true);

useEffect(() => {
  async function getData() {
    await fetch(import.meta.env.VITE_PRIVATE_WEBSITE_COLLECTION_URL)
      .then((res) => res.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      });
  }
  getData();
}, []);

// Returns skeleton loader quickly before render tree proceeds
if (loading) {
  return <SkeletonHome />;
}
```

---

## 8. Progressive Web App (PWA) Implementation
**How:** Native caching strategies are enabled with the injection of service workers from `virtual:pwa-register`.
**Why:** This elevates WebTree beyond a flat website into an installable application directly on users' operating systems/phones. It provides robust offline caching, meaning resources already loaded won't need to be fetched via repeated network pings.

```javascript
/* src/main.jsx */
import { registerSW } from "virtual:pwa-register";

// Immediately registers the service worker upon app initialization
registerSW({ immediate: true });
```
