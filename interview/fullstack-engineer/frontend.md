# Fullstack Engineer - Frontend Questions

Here is a list of questions that you can use to interview potential candidates for a Fullstack Engineer - Frontend position.

**1. What is a difference between `let`, `const` and `var`?**

- These are the three ways to declare a variable in JavaScript.

- `var` declarations are globally scoped or function/locally scoped. The scope is global when a var variable is declared outside a function. This means that any variable that is declared with var outside a function block is available for use in the whole window. But `var` variable causes hoisting issues. Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their containing scope before code execution.

- `let` is block scoped. A block is a chunk of code bounded by {}. A block lives in curly braces. Anything within curly braces is a block. `let` can be updated but not re-declared. Just like `var`, `let` declarations are hoisted to the top. Unlike `var` which is initialized as `undefined`, the let keyword is not initialized. So if you try to use a let variable before declaration, you'll get a `Reference Error`.

- Variables declared with the `const` maintain constant values. `const` declarations share some similarities with let declarations.
`const` variable declarations are block scoped.  `const` variable cannot be updated or re-declared

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
        increment: function() {
            count++;
            return count;
        },
        decrement: function() {
            count--;
            return count;
        },
        getCount: function() {
            return count;
        }
    };
}

const counter = createCounter();
console.log(counter.increment()); // Output: 1
console.log(counter.increment()); // Output: 2
console.log(counter.decrement()); // Output: 1
console.log(counter.getCount());  // Output: 1
// console.log(counter.count);     // Undefined - count is private
```

**4. What are the benefits of using a CSS preprocessors like SASS or LESS?**

**5. How do you optimize a web page for performance ?**

**6. What is the difference between `flexbox` and CSS grid? When would you use one over the other?**

**7. How does the event delegation work in JavaScript?**

**8. What are Progressive Web Apps(PWAs) and what technologies are used to build them?**

**9. Explain how the browser renders a webpage(Critical Rendering Path)?**

**10. How do you ensure you UI is accessible(WCAG standards)?**
