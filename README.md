# Nested Relationships

## Make a nested array

```js
const data = [
  { id: 1, parent: 0, text: "Top-level comment 1" },
  { id: 2, parent: 0, text: "Top-level comment 2" },
  { id: 3, parent: 1, text: "Reply to Top-level comment 1" },
  { id: 4, parent: 3, text: "Reply to Reply to Top-level comment 1" },
];

/**
 * Restructure the flat data array into a nested array.
 *
 * @param {array} data
 * @returns {array}
 */
function restructureArray(data) {
  // Create a map of the data array
  const dataMap = {};
  // Create an array to hold the root elements
  const root = [];

  // Iterate through the data array and add each item to the map
  // with its ID as the key and add an empty children array.
  data.forEach((item) => {
    dataMap[item.id] = {
      ...item,
      children: [],
    };
  });

  // Iterate through the data array again. If the item has a parent,
  // add it as a child of its parent. If it doesn't have a parent,
  // it's a root element and should be added to the `root` array.
  data.forEach((item) => {
    const parent = dataMap[item.parent];
    if (parent) {
      parent.children.push(dataMap[item.id]);
    } else {
      root.push(dataMap[item.id]);
    }
  });

  return root;
}

const result = restructureArray(data);

// Output the resut array as a tree.
console.log(JSON.stringify(result, null, 2));
```

## Add nested comments

```js
const data = [
  { id: 1, parent: 0, text: "Top-level comment 1" },
  { id: 2, parent: 0, text: "Top-level comment 2" },
  { id: 3, parent: 1, text: "Reply to Top-level comment 1" },
  { id: 4, parent: 3, text: "Reply to Reply to Top-level comment 1" },
];

/**
 * Restructure the flat data array into a nested array.
 *
 * @param {array} data
 * @returns {array}
 */
function restructureArray(data) {
  // Create a map of the data array
  const dataMap = {};
  // Create an array to hold the root elements
  const root = [];

  // Iterate through the data array and add each item to the map
  // with its ID as the key and add an empty children array.
  data.forEach((item) => {
    dataMap[item.id] = {
      ...item,
      children: [],
    };
  });

  // Iterate through the data array again. If the item has a parent,
  // add it as a child of its parent. If it doesn't have a parent,
  // it's a root element and should be added to the `root` array.
  data.forEach((item) => {
    const parent = dataMap[item.parent];
    if (parent) {
      parent.children.push(dataMap[item.id]);
    } else {
      root.push(dataMap[item.id]);
    }
  });

  return root;
}

const comments = restructureArray(data);
console.log(JSON.stringify(comments, null, 2));

/**
 * Generate a nested text string from the nested array.
 * @param {*} comments
 * @param {*} level
 * @returns {string}
 */
function generateNestedText(comments, level = 0) {
  let output = "";

  // Iterate through the comments array and add each comment's text
  comments.forEach((comment) => {
    // Create an indent string based on the current level
    let indent = "-".repeat(level + 1) + " ";

    // Add the comment text to the output string
    output += indent + comment.text + "\n";

    // If the comment has children, recursively call this function
    if (comment.children && comment.children.length > 0) {
      output += generateNestedText(comment.children, level + 1);
    }
  });

  return output;
}

const result = generateNestedText(comments);

console.log(result);
```

## Generate nested list html

```js
// JavaScript code​​​​​​‌‌​​‌​​‌‌​‌‌‌​‌​​‌‌‌​​‌​​ below
// Change these values to control whether you see 
// the expected answer and/or hints.
const showExpectedResult = false
const showHints = false

const comments = [
  {
    comment_ID: 1,
    comment_text: "Top-level comment 1",
    comment_parent: 0,
  },
  {
    comment_ID: 2,
    comment_text: "Top-level comment 2",
    comment_parent: 0,
  },
  {
    comment_ID: 3,
    comment_text: "Reply to Top-level comment 1, Child comment 1",
    comment_parent: 1,
  },
  {
    comment_ID: 4,
    comment_text: "Reply to Top-level comment 1, Child comment 2",
    comment_parent: 1,
  },
  {
    comment_ID: 5,
    comment_text: "Reply to Top-level comment 1, Child comment 3",
    comment_parent: 1,
  },
  {
    comment_ID: 6,
    comment_text: "Reply to Top-level comment 2, Child comment 1",
    comment_parent: 2,
  },
  {
    comment_ID: 7,
    comment_text: "Reply to Top-level comment 2, Child comment 2",
    comment_parent: 2,
  },
  {
    comment_ID: 8,
    comment_text: "Reply to Top-level comment 2, Child comment 3",
    comment_parent: 2,
  },
  {
    comment_ID: 9,
    comment_text: "Reply to Reply to Top-level comment 1, Grandchild comment 1",
    comment_parent: 3,
  },
  {
    comment_ID: 10,
    comment_text: "Reply to Reply to Top-level comment 1, Grandchild comment 2",
    comment_parent: 3,
  },
  {
    comment_ID: 11,
    comment_text: "Reply to Reply to Top-level comment 1, Grandchild comment 3",
    comment_parent: 3,
  },
  {
    comment_ID: 12,
    comment_text: "Reply to Reply to Top-level comment 1, Grandchild comment 4",
    comment_parent: 3,
  },
  {
    comment_ID: 13,
    comment_text: "Reply to Reply to Top-level comment 1, Grandchild comment 5",
    comment_parent: 3,
  },
  {
    comment_ID: 14,
    comment_text: "Reply to Reply to Top-level comment 1, Grandchild comment 6",
    comment_parent: 3,
  },
  {
    comment_ID: 15,
    comment_text: "Reply to Reply to Top-level comment 1, Grandchild comment 7",
    comment_parent: 3,
  },
];

// Restructure the comments array into a nested object
function restructureComments(comments) {
  const commentsMap = {};
  const rootComments = [];

  // Create a map of comments by their ID
  comments.forEach((comment) => {
    commentsMap[comment.comment_ID] = {
      ...comment,
      children: [],
    };
  });

  // Iterate through the comments again and add each one as a child
  // of its parent comment, if it has one. If it doesn't have a parent,
  // it's a root-level comment and should be added to the `rootComments` array.
  comments.forEach((comment) => {
    if (comment.comment_parent !== 0) {
      const parent = commentsMap[comment.comment_parent];
      if (parent) {
        parent.children.push(commentsMap[comment.comment_ID]);
      }
    } else {
      rootComments.push(commentsMap[comment.comment_ID]);
    }
  });

  return rootComments;
}

// Generate the nested list HTML
function generateNestedList(comments,  document) {

  const ul = document.createElement('ul')

  // Iterate through the comments array and add each comment's text
  comments.forEach((comment) => {
    const li = document.createElement('li')
    li.textContent = comment.comment_text
    if (comment.children && comment.children.length > 0) {
      li.classList.add('has-submenu')
      const nestedUl = generateNestedList(comment.children,  document)
      li.appendChild(nestedUl)
    }
    ul.appendChild(li)
  });

  return ul

}
```

# Classes and inheretance

## Create a library with books

## Users managing other users

# Singletons and Proxy Objects

## Create a logging system

## Data validation system

# Observer pattern

## Temperature display

## Stock information

# Reactive objects and Factories

## Create a reactive shopping cart

## Create a reactive object



