# Fullstack Engineer - Frontend Questions

Here is a list of questions that you can use to interview potential candidates for a Fullstack Engineer - Frontend position.

**1. What is a difference between `let`, `const` and `var`?**

- These are the three ways to declare a variable in JavaScript.

- `var` declarations are globally scoped or function/locally scoped. The scope is global when a var variable is declared outside a function. This means that any variable that is declared with var outside a function block is available for use in the whole window. But `var` variable causes hoisting issues. Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their containing scope before code execution.

- `let` is block scoped. A block is a chunk of code bounded by {}. A block lives in curly braces. Anything within curly braces is a block. `let` can be updated but not re-declared. Just like `var`, `let` declarations are hoisted to the top. Unlike `var` which is initialized as `undefined`, the let keyword is not initialized. So if you try to use a let variable before declaration, you'll get a `Reference Error`.

- Variables declared with the `const` maintain constant values. `const` declarations share some similarities with let declarations.
  `const` variable declarations are block scoped. `const` variable cannot be updated or re-declared

**2. How doe the CSS Box model work, and how do you handle spacing issue ?**

- The CSS box model is essentially a box that wraps around every HTML element. It consists of: content, padding, borders and margins. The image below illustrates the box model:
  - **Content** - The content of the box, where text and images appear
  - **Padding** - Clears an area around the content. The padding is transparent
  - **Border** - A border that goes around the padding and content
  - **Margin** - Clears an area outside the border. The margin is transparent

**3. Explain the concept of closures in JavaScript with an example.**

- In JavaScript, a closure is a feature that allows a function to "remember" the environment (or scope) in which it was created, even after that scope has finished executing. This means the function retains access to variables from its outer scope, even when it’s invoked outside of that scope. Closures are a fundamental concept in JavaScript and are often used for data privacy, callbacks, and functional programming patterns.

- When a function is defined inside another function, the inner function forms a closure over the outer function’s variables. This happens because JavaScript uses **lexical scoping**, where the scope of a variable is determined by its position in the source code. The inner function retains a reference to the outer function’s variables, even after the outer function has completed execution.

```js
function createCounter() {
  let count = 0; // Private variable

  return {
    increment: function () {
      count++;
      return count;
    },
    decrement: function () {
      count--;
      return count;
    },
    getCount: function () {
      return count;
    },
  };
}

const counter = createCounter();
console.log(counter.increment()); // Output: 1
console.log(counter.increment()); // Output: 2
console.log(counter.decrement()); // Output: 1
console.log(counter.getCount()); // Output: 1
// console.log(counter.count);     // Undefined - count is private
```

**4. What are the benefits of using a CSS preprocessors like SASS or LESS?**

- CSS preprocessors like SASS (Syntactically Awesome Style Sheets) and LESS (Leaner Style Sheets) extend the functionality of vanilla CSS by introducing features that make styling more efficient, maintainable, and scalable. These tools process their own syntax into standard CSS that browsers can interpret.

- **Benefits of using CSS preprocessors:**

  - **Variables:** Preprocessors allow you to define variables to store colors, font stacks, or any CSS value that can be reused throughout your stylesheets. This makes it easier to update styles across your site by changing a single variable.
  - **Nesting for Better Readability:** Preprocessors allow you to nest your CSS selectors, which can be useful for organizing your styles and making your code more readable.
  - **Mixins for Reusable Code Blocks:** Mixins are reusable blocks of styles that can be included within other selectors. This can help reduce redundancy in your stylesheets and make it easier to maintain consistent styles.
  - **Functions:** Preprocessors allow you to define functions that can accept arguments and return values. This can be useful for creating complex styles or calculations.
  - **Modularity with Partials and Imports:** Preprocessors allow you to split your stylesheets into separate files and import them into a main stylesheet. This can help organize your code and make it easier to manage.
  - **Modular Architecture:** Preprocessors allow you to break your stylesheets into smaller, modular files, which can be compiled into a single stylesheet. This can help improve performance by reducing the number of HTTP requests needed to load your styles.
  - **Control Directives:** You can use logic like if-statements and loops to generate styles programmatically.

- While preprocessors offer significant advantages, they introduce a build step (compiling to CSS), which adds complexity to the development pipeline. However, modern tools like Webpack, Vite, or CLI compilers (e.g., sass or lessc) make this seamless.

- **SASS:** More feature-rich (e.g., @for, @if, SCSS syntax), widely adopted, and has two syntaxes (SCSS and indented).
- **LESS:** Simpler, runs in the browser with a JS library (though not recommended for production), and has slightly less functionality.

**5. How do you optimize a web page for performance ?**

- Optimizing a web page for performance involves improving its speed, responsiveness, and efficiency to enhance user experience, reduce bounce rates, and improve search engine rankings. Performance optimization spans front-end, back-end, and network considerations.

  **1. Minimize and Optimize Assets** - **Minify CSS, JavaScript, and HTML:** Remove unnecessary characters (whitespace, comments) using tools like UglifyJS, Terser, or CSSNano. - Example: A 100KB un-minified JS file might shrink to 60KB. - **Compress Images**: Use formats like WebP or AVIF, and tools like `ImageOptim` or `Squoosh` to reduce file sizes without losing quality. - Example: A 1MB PNG could be compressed to 200KB in WebP. - **Use CSS Sprites**: Combine multiple small images into one sprite sheet to reduce HTTP requests. - **Lazy Load Assets:** Load images, videos, or scripts only when they enter the viewport using the loading="lazy" attribute or JavaScript Intersection Observer.
  **2. Reduce HTTP Requests** - **Bundle Files:** Combine multiple CSS or JS files into a single file using build tools like Webpack or Vite. - Why: Fewer requests mean faster page loads. - **Inline Critical CSS:** Embed essential CSS directly in the `<head>` to render above-the-fold content faster, deferring non-critical styles. -

  **3. Leverage Browser caching** - **Set Cache Headers:** Use Cache-Control and ETag headers to cache static assets (e.g., images, CSS, JS) in the browser. - Example: `Cache-Control: max-age=31536000` for a 1-year cache. - **Use Service Workers:** Cache assets for offline use and faster subsequent loads with a service worker. - **CDN Usage:** Serve assets from a Content Delivery Network (CDN) to cache files closer to users and reduce latency.
  **4. Optimize Rendering Performance** - **Reduce Reflows and Repaints:** Minimize DOM manipulations and use CSS transforms (`translate`, `scale`) instead of properties like top or left. - **Use GPU Acceleration:** Apply will-change or transform: translateZ(0) to offload animations to the GPU. - **Debounce/Throttle Events:** Limit the frequency of expensive operations like scroll or resize listeners. - **Prioritize Critical Rendering Path:** Ensure the browser can render content quickly by optimizing the order of resource loading (HTML → CSS → JS).
  **5. Improve Server-side Performance** - **Enable Compression:** Use Gzip or Brotli to compress text-based assets (HTML, CSS, JS) before sending them to the client. - Example: A 50KB CSS file might compress to 10KB - **Optimize Database Queries:** Index tables, avoid unnecessary joins, and cache query results (e.g., with Redis). - **Use a Fast Server:** Optimize back-end code (e.g., Node.js event loop efficiency) and choose performant hosting (e.g., Nginx over Apache). - **Server-Side Rendering (SSR):** Pre-render pages for faster initial loads, especially for SEO-heavy sites.
  **6. Adopt Modern Technologies** - **HTTP/2 or HTTP/3:** Enable multiplexing and header compression to reduce latency compared to HTTP/1.1. - **Tree Shaking:** Remove unused code from JS bundles during builds (e.g., with Rollup or Webpack). - **Code Splitting:** Split JS into smaller chunks loaded on demand (e.g., React.lazy, dynamic imports).
  **7. Measure and Monitor** - **Use Performance Tools:** Analyze with Lighthouse, WebPageTest, or Chrome DevTools to identify bottlenecks (e.g., Time to First Byte, First Contentful Paint). - **Set Performance Budgets:** - **Real User Monitoring (RUM):**

- **Practical Example:**

  - Imagine a page with a 2MB unoptimized image, 10 JS files, and render-blocking CSS:
    - Before: 5s load time, 15 HTTP requests.
    - After Optimization:
      - Compress image to 200KB WebP, lazy-load it.
      - Bundle JS into 1 file (minified), defer it.
      - Inline critical CSS, defer non-critical styles.
      - Enable Brotli and caching.
      - Result: 1.5s load time, 5 HTTP requests.

- **Key Metrics to Target:**

  - **First Contentful Paint (FCP):** < 1.8s (content appears).
  - **Time to Interactive (TTI):** < 5s (page is fully usable).
  - **Largest Contentful Paint (LCP):** < 2.5s (main content loads).
  - **Cumulative Layout Shift (CLS):** < 0.1 (visual stability).

**6. What is the difference between `flexbox` and CSS grid? When would you use one over the other?**

Flexbox (Flexible Box Layout) and CSS Grid are both powerful layout systems in CSS, but they serve slightly different purposes and have distinct characteristics:

- **Main differences:**

  - **1. Dimensionality:**
    - **Flexbox:** One-dimensional layout system. It works primarily along a single axis—either a row (horizontal) or a column (vertical). It’s designed to distribute space and align items in one direction at a time.
    - **CSS Grid:** Two-dimensional layout system. It allows you to define both rows and columns, creating a grid of intersecting tracks. This makes it ideal for complex layouts with rows and columns.
  - **2. Purpose:**
    - **Flexbox:** Best suited for laying out items in a single direction. It’s great for creating flexible and dynamic layouts, like navigation menus, card components, or centering elements.
    - **CSS Grid:** Ideal for creating grid-based layouts with rows and columns. It’s perfect for designing complex web pages with multiple sections, such as magazine layouts or image galleries.
  - **3. Content vs Layout:**
    - **Flexbox:** Content-driven. The size and arrangement of items depend heavily on the content inside them, and Flexbox adjusts dynamically to accommodate it.
    - **CSS Grid:** Layout-driven. You define the structure (rows and columns) first, and then place items into that predefined grid, giving you more control over the overall design.
  - **4. Item placement:**
    - **Flexbox:** Items are placed automatically along the main axis, with limited control over exact positioning unless you use margins or hacks.
    - **CSS Grid:** You can explicitly place items anywhere on the grid using line numbers, named areas, or spans, offering precise control.
  - **5. Alignment**
  - **6. Complexity**

- **When to use Flexbox vs CSS Grid**
  - Flexbox: Use for simpler, linear layouts where content drives the design.
  - CSS Grid: Use for complex, grid-based layouts where the structure is predefined.

**7. How does the event delegation work in JavaScript?**

Event delegation in JavaScript uses event bubbling to handle events efficiently. Instead of attaching event listeners to individual elements, you attach a single listener to a parent element. When an event occurs on a child element, it bubbles up to the parent, and the listener checks the event’s target (e.g., using `event.target`) to determine which child triggered it. This reduces memory usage and simplifies dynamic element handling.

- **Example: Click on list item**

  ```html
  <ul id="list">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
  <script>
    document.getElementById('list').addEventListener('click', (event) => {
      if (event.target.tagName === 'LI') {
        console.log(event.target.textContent); // Logs clicked item's text
      }
    });
  </script>
  ```

  - A single lister on the `<ul>` element captures all click events on its children `<li>` items.

**8. What are Progressive Web Apps(PWAs) and what technologies are used to build them?**

**PWAs** are web applications that combine the best of web and native app experiences. They’re fast, reliable, and work offline, offering features like push notifications and home-screen installation.

- **Technologies Used**

  - HTML, CSS, JavaScript: Core web technologies for structure, styling, and functionality.
  - Service Workers: JavaScript files that run in the background to enable offline caching, push notifications, and background sync.
  - Web App Manifest: A JSON file (e.g., manifest.json) that defines the app’s metadata (name, icons, theme) for installability.
  - HTTPS: Ensures secure communication, required for Service Workers.
  - Fetch API: Handles network requests, often used with Service Workers for caching.

**9. Explain how the browser renders a webpage(Critical Rendering Path)?**

The Critical Rendering Path is the sequence of steps a browser takes to convert HTML, CSS, and JavaScript into a visible webpage. Understanding it helps optimize performance by minimizing the time to first render. Here’s a detailed breakdown:

1. Request and Response

   - The browser sends a request to the server for the HTML file (e.g., index.html) when a user enters a URL.
   - The server responds with the HTML content.

2. Building the DOM (Document Object Model)

   - The browser parses the HTML, starting from the top, and constructs the DOM tree.
   - It reads tags (e.g.,`<div>`, `<p>`) and their content, creating a tree of nodes representing the document structure.
     If it encounters external resources (e.g., `<script src="...">` or `<link rel="stylesheet">`), it may pause parsing to fetch them, unless they’re marked async or defer (for scripts).

3. Building the CSSOM (CSS Object Model)

   - The browser fetches and parses CSS files (or inline `<style>` tags) to create the CSSOM tree.
   - Like the DOM, it’s a tree structure representing styles and their hierarchy (e.g., selectors and properties like color: blue).
   - CSS parsing is render-blocking: The browser waits until the CSSOM is complete before proceeding, as styles determine how elements look.

4. Combining DOM and CSSOM into the Render Tree

   - The browser merges the DOM and CSSOM into the Render Tree.
   - The Render Tree includes only visible content (e.g., excludes `<head>`, display: none elements) and applies styles to each node.
   - This step determines what will be displayed and how it will look.

5. Layout (Reflow)

   - The browser calculates the exact position and size of each element in the - Render Tree based on the viewport size and CSS properties (e.g., width, margin, position).
   - This process, called layout or reflow, assigns coordinates (x, y) and dimensions to every node.
   - It’s resource-intensive and re-triggered by changes like resizing the window or modifying the DOM.

6. Painting

   - The browser converts the Render Tree into pixels on the screen in the paint step.
   - It draws elements layer by layer (e.g., backgrounds, borders, text) using the GPU for efficiency.
   - The result is the final visual output users see.

7. JavaScript Execution (if applicable)

   - If JavaScript is present, it can run during or after DOM/CSSOM construction (depending on `<script>` placement or attributes like async/defer).
   - JS can modify the DOM or CSSOM, potentially triggering reflow and repaint, which delays rendering.

Critical Rendering Path in Summary

- HTML → DOM
- CSS → CSSOM
- DOM + CSSOM → Render Tree
- Render Tree → Layout (position/size)
- Layout → Paint (pixels on screen)

Optimization Tips

- Minimize render-blocking resources: Use async/defer for scripts, inline critical CSS.
- Reduce file sizes: Compress HTML, CSS, and JS.
- Prioritize visible content: Load above-the-fold content first.
- Avoid reflows: Limit DOM/CSS changes after initial render.

The CRP is all about efficiency—faster DOM/CSSOM construction and fewer reflows/repaints mean quicker page loads!

**10. How do you ensure you UI is accessible(WCAG standards)?**

To make a UI accessible per WCAG (Web Content Accessibility Guidelines) standards, follow these key principles and techniques:

**1. Perceivable:**

- **Text Alternatives:** Provide alt text for images, transcripts for audio/video, and labels for form elements.
- **Adaptable Content:** Ensure content is readable and operable in different formats (e.g., resizable text).
- **Distinguishable:** Use sufficient color contrast, clear typography, and distinguishable elements.

**2. Operable:**

- **Keyboard Accessible:** Ensure all functionality is available via keyboard navigation (e.g., Tab key).
- **Focus Indicators:** Make focus states visible (e.g., :focus { outline: 2px solid blue; }).
- **No Time Traps:** Avoid content that traps users (e.g., modals without close options) or relies on strict timing.
- **Skip Links:** Add "Skip to Content" links for screen readers (e.g., `<a href="#main">`Skip to main content`</a>`).

**3. Understandable**
Consistent Navigation: Keep menus and layouts predictable across pages.
Clear Labels: Use descriptive labels for forms (e.g., <label for="name">Name:</label>).
Error Handling: Provide clear, specific error messages (e.g., "Please enter a valid email").
Language: Declare the page language (e.g., <html lang="en">).
