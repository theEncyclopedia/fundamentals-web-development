# JavaScript modules

JavaScript modules are a way of managing and organizing JavaScript code. Before the introduction of modules, JavaScript files were often organized by separating code into multiple files and including them in an HTML file with script tags. This approach had some limitations, such as the lack of dependency management and namespace collisions. JavaScript modules solve these problems by introducing a way to define, import, and export code.

There are 2 kinds of exports:

- Named exports
- Defaults exports

You can have multiple named exports per module but only one default export.

One thing to note is that JavaScript modules are static, meaning that all import and export statements are hoisted and processed before the code is executed. This allows for static analysis and has some performance benefits, but it also means that you can't conditionally import or export modules.

## Example

```js
// myModule.js
export const name = "OpenAI";

export function sayHello() {
  return `Hello from ${name}!`;
}

export default function () {
  return "This is the default export";
}
```

You can then import these values into another JavaScript file:

```js
// app.js
import defaultExport, { name, sayHello } from "./myModule.js";

console.log(name); // logs "OpenAI"
console.log(sayHello()); // logs "Hello from OpenAI!"
console.log(defaultExport()); // logs "This is the default export"
```
