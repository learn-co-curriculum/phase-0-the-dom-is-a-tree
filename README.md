# The DOM Is a Tree

## Learning Goals

1. Describe how the DOM works as a tree
2. Define the computer science version of "Tree"
3. Ask the DOM to find or "select" an HTML element or elements in the rendered page

## Introduction

Recall that DOM programming is using JavaScript to:

1. Ask the DOM to find an HTML element or elements in the rendered page
2. Remove the selected element(s) or add a new element next to the selected element
3. Adjust a property of the selected element(s)

In previous lessons we were given the command to find the HTML element we
wanted to delete:

```javascript
document.querySelector( selector ).remove()
```

In this lesson, we'll learn the _methods_ on the DOM we need to use to find (or
"select") the HTML element(s) we want to change. In later lessons we'll learn
other methods, like `remove()`, to change the elements.

To understand those "finding" _methods_, we need to take a quick moment to talk
about how the DOM tree (i.e. what we see in the 'Elements' panel of our
DevTools) is used to help the DOM's _methods_ find the right nodes.


## Define the Computer Science Version of "Tree"
- The head of the DOM tree is at the top, and the roots descend from there
- The leaves of the DOM tree are nested HTML Elements
- Thicker branches hold more data

![DOM Tree Graphic](https://curriculum-content.s3.amazonaws.com/skills-front-end-web-development/js-dom-and-events-the-dom-is-a-tree-readme/DOM-model.svg)

## Describe How the DOM Works as a Tree
- Trees can be parents
- DOM begins at `<html>`, but we really only ever change what's in the `<body>` tag
- Give some simple tree examples

## Ask the DOM To Find Or "select" An HTML Element or Elements in the Rendered Page
For all of the following selectors, fill out simple walk-through examples. This lesson exists in Skills but it's *very* dense.


#### `document.getElementById()`
- Since IDs must be unique, this method will only return one element.
- Keep selectors unique
- 

#### `document.getElementsByClassName()`
- Returns an `HTMLCollection` (a list of DOM nodes, _not_ an array), although you can iterate over it with a for loop
- As `className` does not need to be unique, it finds elements by their `className`.


#### `document.getElementsByTagName()`

- Retrieves element by TagName (e.g. `div`, `h1`, `header`, etc.)
- Returns an `HTMLCollection`
- Can iterate through using a for loop

### Finding a Node Without Knowing Anything About It
- What if we are given a tree without any more information about a selector?
- Can chain methods together to select the appropriate node
- Add in appropriate examples

## Conclusion

Understanding the tree structure of the DOM helps us navigate all kinds of
trees. In subtrees and branches we can find the nodes we need by IDs, class
names or tag names. Once we've selected our elements, we can use JavaScript to
manipulate them. By using these techniques, we can start to build a more rich
user experience.

## Resources

- [MDN - Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
