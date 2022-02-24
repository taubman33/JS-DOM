[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)


# The DOM & JavaScript



## Learning Objectives

- Explain what the DOM is and how it is structured
- Target DOM elements using JavaScript selectors
- Create, read, update, and delete DOM elements
- Change the attributes or content of a DOM element
- Explore JavaScript methods for DOM manipulation and traversal

## Framing (10 minutes / 0:10)

In the Objects & Context lesson, you learned about objects as data structures
and how we can use them to store data and methods. Today, we will learn about
how JavaScript uses objects to represent what you see in the browser. Remember,
everything is an object!

The
[Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction),
commonly referred to as the "DOM", is a programming interface for HTML. When you
load HTML into the browser, it gets converted into a dynamic object-based
structure. The [visual representation](https://css-tricks.com/dom/) of this is
what you see when you open up Developer Tools in the browser.

The DOM is available for us to manipulate as an object, and this object is
structured and stored like an upside down tree, like this...

![lxf118 tut_grease diagram](https://git.generalassemb.ly/storage/user/6376/files/1035f642-6263-11e7-9a38-4db66c999724)

Or this...

```
html
└── head
│   ├──title
│   ├──meta
│   ├──link[rel="stylesheet"]
|   └──script[type="text/javascript"]
|
└── body
    ├── header
    │   ├── h1
    │   └── nav
    └── section.1
    |   └── h2
    │   └── article
    ├── section.2
    |   └── h2
    │   └── article
    │       └── block_quote
    │       └── block_quote
    └── footer
```

### The Document Object

Each web page loaded in the browser has its own `document` object. The
`document` interface serves as an entry point to the web page's content. The
document is an example of a **host object**--that is, a JavaScript object
provided by and unique to the browser environment.

Remember when we console.log'ed an object out of context, and we got information about the "Window" scope? That is the same level of Scope that the Document in the DOM is referring to -> literally *everything* going on on the screen

### Nodes

Everything in the DOM exists as a **node**. HTML elements are called **element
nodes**, attributes are called **attribute nodes**, the text inside elements are
called **text nodes**. There are even comment nodes for
`<!-- html comments like this one --->`. The document itself is called a
document node.

You also can refer to nodes by their relationships to each other. For example,
in the graphic above, you would say that the body element is the "parent" to the
two `div` elements contained inside it, which are called child nodes. The two
divs are also "siblings" to one another because they are on the same level in
the tree structure.

## Basics of Working with the DOM (5 min / 0:15)

Understanding the DOM is central to working in JavaScript. JavaScript uses the
DOM to create dynamic HTML. This includes adding new HTML elements and
attributes, changing CSS styles in a page, removing existing elements and
attributes, and [many more things](https://www.w3schools.com/js/js_htmldom.asp).

Most of what you do with client-side javascript is going to revolve around
manipulating the DOM.


We will be using Manipulating the DOM in Real Time in our Event Listeners class later today - clicking buttons to change background color and other CSS style options!

## Getting Data from the DOM

There are two groups of methods you can use to get elements from the DOM. We'll
start with the oldest and end with the ones we recommend.

### `getElement(s)By` (15 min / 0:30)

Each of these methods follows the same general naming convention:

| Method Name                 | Description                                           |
| --------------------------- | ----------------------------------------------------- |
| `.getElementById()`         | Gets a single element by an ID selector               |
| `.getElementsByClassName()` | Gets a list of elements with a class selector         |
| `.getElementsByTagName()`   | Gets a list of elements with a tag (element) selector |

Each of these three methods are part of the `document` object. We'll walk
through each individually:

**`getElementById()`**

To use the `getElementById` method, we first need to reference the `document`
object (where the method lives). Then, we pass in a string that matches the ID
of an element in our HTML

```js
let titleElement = document.getElementById("title");

titleElement.innerHTML = "Hello!"
```


The above code will start at the document (top of the tree), and look for an
element with an id called `title` and save it in the variable `titleElement`

We can then edit the HTML within the document ('innerHTML') to whatever we would like

Now we can begin to code *dynamic* sites, with content that can change each time we load them up!

```js

let name = prompt('what is your name?')

titleElement.innerHTML = `Hello ${name}!`
```


**`getElementsByClassName`**

The `getElementById` method returns a single Node item; the
`getElementsByClassName` returns a NodeList, which is like an Array of Nodes.

```js
let classElements = document.getElementsByClassName("text");
console.log(classElements)
```
We are not going to update every 'Text' class element here, instead we will log all of them into the console

The above code snippet returns a NodeList (like an Array) of every element with
a class of 'text' and saves it to the `classElements` variable. Notice
that `Elements` in the method name is plural here, where as in `getElementById`
it's singular? This is to tell us that `getElementByID` only returns one Node
while `getElementsByClassName` returns a list of Nodes.

**`getElementsByTagName`**

The `getElementsByTagName` is a hand way of retrieving elements by their html
tag (`h1`, `img`, `a`, `li`, etc). `Elements` is plural in the method name,
meaning it too returns a list of Nodes.

```js
let imgElements = document.getElementsByTagName("img");

```

The above snippet returns every `img` element on the page and saves it to the
`imgElements` variable.



### `querySelector` (10 min / 0:50)

There are only two methods in this group: `querySelector` and
`querySelectorAll`. Unlike the `getElement(s)By` group, these are simpler to
understand - querySelector returns a single value, and querySelectorAll
returns...well...everything that it can find. You can even select multiple IDs
this way.

We'll walk through both `querySelector` and `querySelectorAll`, but first a note
about selectors:

#### Selectors

Unlike with the `getElement(s)By` family of methods, we need to pass a complete
selector to both `querySelector` and `querySelectorAll` - it's in the name!
What's a selector? A selector is a way of targeting a particular element,
something we learned about when we first covered CSS.

The following is a list of CSS selectors and the JavaScript equivalents you
would use with `querySelector`:

| CSS Selector  | JS Selector   |
| ------------- | ------------- |
| `.class-name` | `.class-name` |
| `#some-id`    | `#some-id`    |
| `h1`          | `h1`          |

They're the same! Phew, that's lucky!

The `querySelector` methods were designed to mimic the way we target elements in
CSS, so the selector we pass in is the same we'd use to style that element!

**`querySelector`**

With `querySelector`, we'll pass in a selector for the element we want to
retrieve from the DOM. The element that we get back will be the first element
that matches that selector.

```js
let title = document.querySelector(".title");
```

This is one way we can add Click effects to buttons on our sites!

```js
let button = document.querySelector(".button");
```

We'll only get one element back and it will always be the first element that
matches the selector (in this case, `.title`). If we have more than one element
in the page with that selector and we want to retrieve them all, then we'd use
`querySelectorAll`

**`querySelectorAll`**

With `querySelectorAll`, we'll get back all elements on the page that match the
selector we pass in.

```js
let title = document.querySelectorAll("h2");
```

The above code snippet would return a list of all `h2` elements on the page.

Hey, remember .map from the Array lesson? We can use .map to display a lot of images/other data onto a page, the way Amazon or Ebay display all of their items after a search (and by the way, a Searchbar is basically just a nice UI friendly Filter, isn't it?!)


## Setting Data in the DOM

Now that we know how to get elements from the DOM, it'd probably be helpful to
learn what we can do with them. We'll soon learn about adding event listeners to
DOM elements - a way for us to listen for when some event happens to a node
(like it gets clicked) and then perform some response. But there are many other
things we can do with nodes! Toggle, add or remove classes, change their
styling, animate them, move them from one part of the page to another, replace
their content with new content, etc. The list goes on!

These methods are not going to be used as much as the above ones, especially as we move out of Vanilla JS and into ReactJS. If you are interested in learning all of the ways that we can work with Data and Nodes in the DOM, this link will provide examples for many things that we can do

https://www.w3schools.com/js/js_htmldom_collections.asp

however, if you are just learning JS for the first time now, and don't want to complicate things, don't worry about these and focus more on the InnerHTML and QuerySelector methods.

### Exploring DOM Nodes (45 min / 2:00)

**1. Getting and Setting Attributes**

Remember from our HTML lesson that some elements have attributes: the `a` tag
has an `href` attribute and the `img` tag has a `src` attribute. In JavaScript,
there are ways to access the list of attributes on a node and to get and set
attributes.

Every node object has an `attributes` property where it lists it's attributes
(like `href` and `src`). You can get and set data using the `getAttribute` and
`setAttribute` method.

Look at the `attributes` property of a node. Also look up the `getAttribute` and
`setAttribute` methods and how they work. 

```js 
Element.setAttribute(name, value);
```


We are using the same syntax we had before, but now using the attributes of the elements that we want to set in our parameters, and then using the actual names we want to use in the arguments


```js

var button = document.querySelector("button");

button.setAttribute("name", "helloButton");
button.setAttribute("disabled", "");

```


- What is an attribute?
- How do we access the list of attributes on a node?
- How to we get the value of a particular attribute (like the `href` attribute)?
- How do we add an attribute (like the `name` attribute)?

**2. Class list API**

A very common task in JavaScript is toggling CSS classes. We'll remove a
`.is-hidden` class when the user clicks on something or we'll add an `is-active`
class a navigation element when someone clicks on a hamburger menu.

The way we get and set classes on nodes is with the `classList` API. Every node
has a `classList` property and there are methods we can use to add a class
(`add`), remove a class (`remove`) or toggle a class (`toggle`).

The following are the three methods we can use to work with classes on a DOM node:

`.classList.add()
.classList.remove()
.classList.toggle()
`

Research these methods and think about how they work and why they're useful.


- How can we see the list of classes a node has?
- How can we check to see if a node has a class?
- How can we add a class to a node?
- How can we remove a class from a node?
- How can we toggle a class from a node?

**3. Traversing Nodes**

We'll often have a particular node but need to check it's parents, children or
siblings. Luckily, each node has this information stored within it!

Things get interesting here as we are able to CRUD information, content, and data through our different nodes (this can be a bit more advanced than just making your header say Hello ${Name}!

Look through a node object (by console logging) and see if you can find the following:

- `children` / `childNodes`
- `firstChild` / `firstElementChild`
- `lastChild` / `lastElementChild`
- `nextSibling` / `nextElementSibling` and `previousSibling` /
  `previousElementSibling`
- `parentNode`

What are these properties? What is the difference between children and child
Nodes? What kinds of nodes do you see stored in these properties?

Think about these questions and explore the above list of properties.

**4. Content**

We'll sometimes have an element and want to change the text or html contained
within that element. This is commonly called _templating_ and there are
libraries that will make it a little easier. With the new template literal
syntax in ES6, we can often get away without a templating library. We could just
use the list of properties below to reset the html or text of an element and
interpolate data in to it.

Review these properties of a node:

- `innerHTML` / `outerHTML`
- `innerText` / `outerText`
- `textContent`

What are they? How are they similar? How are they different?

Can we change the html inside of an element?

**5. Dataset**

Part of HTML5 includes the `data-*` attribute: a way for us to attach arbitrary
data to an element. If we define a `div` element with a
`data-name="A Great Div"` attribute, then our `dataset` property inside our node
will be an object with a `name` key holding the string `"A Great Div"`.

```html
<div id="great" data-name="A Great Div"></div>

let div = document.getElementById('great') console.log(div.dataset)
```

Play around with it. Look up the `data-*` attribute and explore the `dataset`
property inside of a node. See how you can create data attributes of your own
and retrieve the data they hold from the `dataset` object.

What happens if you have a property with a name like this?

```html
<div id="great" data-camel-case-is-fun="i agree"></div>
```

**extras:**

**6. Changing the Styling**

Something we may want to perform in JavaScript is updating or changing the
styling of an element using JavaScript. A lot of web animation tools do that and
there are tools for React (which we'll learn about later) that do this so you
can write all your styles in JavaScript.

Obviously, there are more than a few ways of doing any of these functions, but a common style you'll see is 

```js

document.getElementById(id).style.property = new style

```


You can spend a few hours here at https://www.w3schools.com/js/js_htmldom_css.asp learning the different DOM methods, and still only be skimming the surface

Explore the `style` property of a node. What do you see in there? How could we
see the style of an element like, is it `display: block`? Can we change these
style properties, like setting the background color?

