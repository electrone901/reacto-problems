## Tree Traversal 🌴🌳🌴

---

## Interviewer Prompt

Today we will write:
- `breadthFirst`
- `depthFirstPreOrder`

(if time allows)

- `depthFirstPostOrder`

Each of these functions will take a node and a callback that prints the node value.

---

## Setup

```javascript
function node(value) {
  return {
    value,
    children: [],
  };
}
const a = node('a');
const b = node('b');
const c = node('c');
const d = node('d');
const e = node('e');
const f = node('f');
const g = node('g');
const h = node('h');
const i = node('i');
const j = node('j');
const k = node('k');
const l = node('l');
const m = node('m');

a.children.push(b, c, d);
b.children.push(e);
e.children.push(k, l);
c.children.push(f, g, h);
h.children.push(m);
d.children.push(i, j);
```

---

## Example

![tree](https://www.cpp.edu/~ftang/courses/CS241/notes/images/trees/tree1.bmp)

| Algorithm             | Order                       | Explanation                                                |
| --------------------- | --------------------------- | ---------------------------------------------------------- |
| `breadthFirst`        | `A B C D E F G H I J K L M` | Each "level" of the tree is printed in order               |
| `depthFirstPreOrder`  | `A B E K L C F G H M D I J` | Children nodes are visited before sibling nodes            |
| `depthFirstPostOrder` | `K L E B F G M H C I J D A` | A node is not traversed until all its children are reached |

---

class: center middle

## Interviewer Guide

---

### RE

- This differs from the traversal we worked on in junior phase in that each node may have any number of children

- You may need to remind your interviewee of what the different types of traversal mean

- Interviewee does not need to write the "node" function, but should be aware of the structure of a node

- Be sure to have your interviewee sketch the example tree

---

### AC
- Remind them that each child of a tree node is it's own tree

---

### TO

- If your interviewee finishes, ask them:
  - What is the Big O of the breadth first? Depth first?

---

## Solution Code (Breadth First)

```javascript
const breadthFirst = (startingNode, callback) => {
  // we use a queue to iterate over the tree
  // progressively adding the children as we go
  // The tree begins with the first node
  const queue = [startingNode];
  // you might want to consider handling edges cases
  /// such as not receiving a properly formatted node
  // or make a proper Node constructor/prototype (see below)
  while (queue.length) {
    // we shift off the array instead of iterating with a counter
    // as we are treating it as a queue (FIFO)
    const node = queue.shift();
    callback(node.value);
    // es6 format:
    queue.push(...node.children);
    // es5 might look like this if queue were a var (or let) instead of const
    // queue = queue.concat(node.children)
    // or:
    // queue.push.apply(queue, node.children)
  }
};
```
## Complexity
- Time Complexity: ?
- Space Complexity: O(n)
---

## Solution Code (Depth First)

```javascript
// depth first seems trivial in comparison! Simply log the value
// and then call the function on each node
const depthFirstPreOrder = (startingNode, callback) => {
  callback(startingNode.value);
  startingNode.children.forEach(child => {
    depthFirstPreOrder(child, callback);
  });
};

const depthFirstPostOrder = (startingNode, callback) => {
  startingNode.children.forEach(child => {
    depthFirstPostOrder(child, callback);
  });
  callback(startingNode.value);
};
```
## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)
