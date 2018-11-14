# The DOM Is a Tree

## Learning Goals

1. Describe how the DOM works as a tree
2. Define the computer science version of "Tree"
3. Ask the DOM to find or "select" an HTML element or elements in the rendered page

## Introduction

DOM programming is using JavaScript to:

1. Ask the DOM to find an HTML element or elements in the rendered page
2. Remove the selected element(s) or add a new element next to the selected element
3. Adjust a property of the selected element(s)

In previous lessons we were given the command to find the HTML element we
wanted to delete:

```javascript
document.querySelector( selector ).remove()
```

In this lesson, we'll learn the `methods` on the DOM we need to use to `select` the HTML element(s) we want to change. In later lessons we'll learn
other methods, like `remove()`, to change the elements.

To understand those `methods`, we first need to talk about how the DOM tree
(i.e. what we see in the 'Elements' panel of our DevTools) is used to help the
DOM's `methods` find the right nodes.


## Define the Computer Science Version of "Tree"

What do we mean when we say that the DOM is a tree? Trees make a good metaphor
for the DOM because almost everyone has seen a tree. Starting at the bottom, you
can climb up the tree and out to the farthest — and smallest — branches. The
thicker a branch is, the stronger its connections are: the more it holds within
it. Likewise, the thinner a branch is, the less it holds inside.

The DOM works basically the same way, except we usually talk about the root as
being at the top of the DOM and the leaves being the most deeply nested HTML
elements. So basically, we can imagine a tree upside down.

![DOM Tree Graphic](https://curriculum-content.s3.amazonaws.com/skills-front-end-web-development/js-dom-and-events-the-dom-is-a-tree-readme/DOM-model.svg)

## Describe How the DOM Works as a Tree
An interesting property of trees is that every tree can contain subtrees,
which we can treat independently of their parent trees. Subtrees are like branches. 

Practically speaking, the DOM begins at `<html>`, but we should avoid changing
what's between the `<head></head>` tags. Most of the time, we will look at the
DOM subtree with its root at `<body>` and only deal with things that will be
visible on the page. Within that tree, we might also deal with subtrees. So, for
example, if we have

``` html
<body>
  <div>
    <p>Hi!</p>
  </div>

  <div>
    <p>Bye!</p>
  </div>
</body>
```

We would have a tree that looks like

``` shell
        body
        /  \
      div   div
      /      \
     p        p
    /          \
 "Hi!"        "Bye!"
```

Pretty simple, right? Similarly, if we had a DOM subtree that looked like

``` html
<div>
  <div>
    <h1>Hello!</h1>
  </div>

  <div>
    <h5>Sup?</h5>
  </div>
</div>
```

We could simply treat it as the tree

``` shell
         div
        /  \
      div   div
      /      \
    h1        h5
    /          \
 "Hello!"     "Sup?"
```

## Ask the DOM To Find Or "select" An HTML Element or Elements in the Rendered Page

Our tree is organized so that a node's metadata doesn't make it harder to find it's children. Not only does providing more information about
a node via HTML make it more useful, it also makes it easier to find.

For the following exercises, you can experiment with any page on the
Internet. It's fun to change "The New York Times" or Facebook.

### Finding a Node

JavaScript exposes a few ways of finding DOM nodes directly, or via other
ways, courtesy of the `document` object.

#### `document.getElementById()`

This method provides the quickest access to a node, but it requires that we know
a very specific piece of information — its `id`. This method can only return one
element, since CSS IDs are expected to be unique.

Given the following DOM tree:

``` html
<div>
  <h5 id="greeting">Hello!</h5>
</div>
```

We could find the `h5` element with `document.getElementById('greeting')`.
Notice how the `id` that we pass to `getElementById` is identical to the `id` in
`<h5 id="greeting">`. You can use either single('') or double("") quotes around
the `id`, as long as you use the same kind to open and close them!

**Try it out!**

Open up your DevTools and find an element on the page — make note of its `id`.
Then open up your console, type `document.getElementById('theIdYouTookNoteOf')`,
and check out your handy-dandy DOM node.

#### `document.getElementsByClassName()`
This one is also very commonly used in DOM programming.

This method finds elements by their `className`. Unlike the previous method,
class names do not need to be unique, so this method returns an `HTMLCollection`
of all the elements with the given class. You can iterate over an
`HTMLCollection` with a simple `for` loop.

Given the following DOM tree:

``` html
<!-- the `className` attribute is called `class` in HTML  -->
<div>
  <div class="banner">
    <h1>Hello!</h1>
  </div>

  <div class="banner">
    <h1>Sup?</h1>
  </div>

  <div class="banner">
    <h5>Tinier heading</h5>
  </div>
</div>
```

We could find all of the elements with the class name "banner" by calling
`document.getElementsByClassName('banner')`.

**Try it out!**

Inspect your web page again, this time making note of a `class`. Get all
elements with that `class` and give 'em a look. On the returned object you
can use the `.length` property to find out how many came back.

If you recall the `for` loop syntax you might try to write a loop which prints
out the `innerHTML` property of every element in the collection. You might find
doing so much easier if you save the results of
`document.getElementsByClassName()` to a variable: `var elements =
document.getElementsByClassName('yourClassNameHere')`.


#### `document.getElementsByTagName()`

If you don't know an element's `id` or `class`, but you do know its tag
name (the tag name is the thing between the `<>`, e.g., `'div'`, `'h1'`,
`header`, `article` etc.).  Since tag names aren't unique, this method returns
an `HTMLCollection` also.

**Try it out!**

Explore the DOM in console by typing `document.getElementsByTagName('div')`.
You can iterate through these elements using a simple `for` loop as well.

### Finding a Node Without Knowing Anything About It
What if we know next to nothing about an element? Or what if we're just
interested in finding out more about the child nodes of a given element? This
is where our knowledge of trees comes in handy!

Given the following DOM tree:

``` html
<main>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
</main>
```

How would we go about changing only the second "Hello!" to "Goodbye!"?

Here we're going to use a hodgepodge of `methods` to accomplish the goal.

Let's start by getting the `<main>` element

``` javascript
const main = document.getElementsByTagName('main')[0]
```

Then we can get the children of `main` using `main.children`, so we can get the
second child with `main.children[1]`.

``` javascript
const div = main.children[1]
```

Finally, we can get and update our `<p>` element with

``` javascript
// we can call getElementsByTagName() on an _element_
// to constrain the search to its children!
const p = div.getElementsByTagName('p')[0]
```

And lastly we can change an attribute on the node. Elsewhere we've shown how to
remove nodes. In this lesson we both get better at finding them and we
change one's attribute!

```javascript
p.textContent = "Goodbye!"
```

Obviously, this way of accessing that text isn't efficient and won't work on all
pages, but it does a good job of demonstrating the basic tools available to us
for finding and manipulating HTML elements.

## Conclusion

Understanding the tree structure of the DOM helps us navigate all kinds of
trees. In subtrees and branches we can find the nodes we need by IDs, class
names or tag names. Once we've selected our elements, we can use JavaScript to
manipulate them. By using these techniques, we can start to build a more rich
user experience.

## Resources

- [MDN - Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
