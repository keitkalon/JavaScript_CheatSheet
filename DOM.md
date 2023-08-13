
## Selecting Elements:

- `document.getElementById('id')`: Get an element by its ID.
- `document.getElementsByTagName('tag')`: Get elements by their tag name.
- `document.getElementsByClassName('classname')`: Get elements by their class name.
- `document.querySelector('selector')`: Get the first matching element for a CSS selector.
- `document.querySelectorAll('selector')`: Get all matching elements for a CSS selector.

## Manipulating Elements:
- `.innerHTML`: Get or set the inner HTML content of an element.
- `.textContent`: Get or set the text content of an element.
- `.setAttribute(name, value)`: Set an attribute's value.
- `.getAttribute(name)`: Get an attribute's value.
- `.removeAttribute(name)`: Remove an attribute from an element.
- `.classList.add('classname')`: Add a class to an element.
- `.classList.remove('classname')`: Remove a class from an element.
- `.classList.toggle('classname')`: Toggle a class.
- `.classList.contains('classname')`: Check if an element contains a certain class.

## Traversing the DOM:
- `.parentNode`: Get the parent node of an element.
- `.previousSibling` and `.nextSibling`: Get the previous or next sibling respectively.
- `.firstChild` and `.lastChild`: Get the first or last child respectively.
- `.childNodes`: Get a NodeList of child nodes.
- `.children`: Get a HTMLCollection of child elements.
- `.firstElementChild` and `.lastElementChild`: Get the first or last child element respectively.

## Creating, Inserting, and Deleting Elements:
- `document.createElement('tag')`: Create a new DOM element.
- `.appendChild(element)`: Append an element as the last child of another.
- `.insertBefore(newElement, referenceElement)`: Insert an element before another.
- `.removeChild(element)`: Remove a child element.
- `element.remove()`: Remove an element directly.

## Events:
- `.addEventListener('event', function)`: Attach an event listener to an element.
- `.removeEventListener('event', function)`: Remove an event listener from an element.

## Styles:
- `.style.propertyName`: Get or set inline styles on an element.

## Others:
- `document.createDocumentFragment()`: Creates a new DocumentFragment.
- `element.cloneNode(true|false)`: Clones a node. If true, it clones with descendants.

## Window and Document Events:
- `window.onload`: Executes when the entire document (including all resources) is fully loaded.
- `document.onreadystatechange`: Check the document's ready state (loading, interactive, complete).
- `document.readyState`: Returns the current ready state of the document.

## Forms:
- `document.forms`: Collection of forms.
- `.submit()`: Submit a form.
- `.reset()`: Reset a form.

## Animations:
- `window.requestAnimationFrame(callback)`: Calls a function to update an animation before the next repaint.
