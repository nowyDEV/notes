# Notes from [The Hard Parts of UI Development](https://frontendmasters.com/courses/hard-parts-ui-dev/introduction/)

## State & View

- Two main goals of UI engineering are: Display UI to the users and let them interact with it
- DOM is a list representation of HTML elements stored as an object in C++ that get displayed on a page thanks to browser's layout and rendering engine.
  DOM and rendering/layout engines are part of Webcore
- CSSOM is an object representation of page styles, layout and rendering engines analyze both DOM and CSSOM before displaying the page
- Every time a user sees the change on a page, the underlying data changes and get's reflected on a screen
- Before the changes on a page get displayed, the C++ DOM needs to be changed first. It's impossible to interact with the C++ code directly, we need to use JavaScript

## JavaScript, DOM & Events

- `document` object can be used to interact with the DOM
- data and the ability to modify it are available only in JavaScript
- Javascript runtime includes thread of execution to run code, memory to store data and call stack & event loop to allow code (functions) to run asynchronously
- WebIDL is used to connect JS with web browser APIs, it is used to define interfaces and methods that can be called from JavaScript to access browser functionality and web APIs.
- WebCore contains the key HTML, CSS, DOM, and layout engine code that handles parsing, styling, and rendering web pages. It is the browser's engine responsible for displaying and interacting with web content, it gives JavaScript an access to the DOM.
- DOM events and handler functions allow for user actions/input to change the data in JavaScript

  ```javascript
  // Assign the JS representation of DOM node input to a variable
  const inputEl = document.querySelector("input");

  function handleInput() {
    // ...
  }
  // Assign handleInput function to `oninput` handler on a JS Node object that is directly linked to a DOM element
  inputEl.oninput = handleInput;

  // Once the user types something in an input, an event is fired that triggets native handler to execute, this handler is connected to the `handleInput` function thanks to a binding with `oninput`. `handleInput`gets pushed to a Callback (task) queue and waits for the main JS Callstack to be empty. Once that happens, it moves to the main Callstack and is executed.
  ```

## Data-Binding in the UI

-

## Virtual DOM

## Composition & Functional Components

## Performance improvements
