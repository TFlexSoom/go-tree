# go-tree
A golang implementation of trees because I end up coding this up myself too often.
I would recommend a more standard library but if you like the implementation feel
free to use this container package.

## Pre-requisites
1. Install Go

## go pkg
`go add go-tree`

## How to test
`go test ./... -v`

## Documentation

### Thread-safety
This container is not threadsafe. Instances must never be shared across instances.

### Creating a tree
You have two choices of implementations. The tree type itself is the same generically.
```go
linkedTree := NewLinkedTree[int]()
graphTree := NewGraphTree[int]()
```

Alternatively you can also suggest a capacity that is used for depth and breadth (the number of slots per child).

```go
linkedTree := NewLinkedTreeCap[int](3, 3)
graphTree := NewGraphTree[int](100, 2)
```

### Using the tree
Trees can be modified with chaining

```go
tree.SetValue(1).AddChild(2).AddChild(3)
```

This would create a tree visually like the following
```
1
|  \
2   3
```

Note: The chaining will always return the root of the tree. If you want a child use the `getChild(index)` function.

```go
childTree := tree.getChild(0)
childTree.AddChild(4).AddChild(5)
// resulting in
/*
  1
 /  \
2    3
| \
4  5

*/
```

### Iteration
There are provided functions for depth and breadth first slice collection

```go
tree := NewGraphTree[string]
tree.SetValue("hello").AddChild("world").AddChild("welcome")
tree.GetValue(0).AddChild("home")

equals(LeftBreadthFirst(tree), []string{"hello", "world", "welcome", "home"}) // true
equals(RightBreadthFirst(tree), []string{"hello", "welcome", "world", "home"}) // true
equals(LeftDepthFirst(tree), []string{"hello", "world", "home", "welcome"}) // true
equals(RightDepthFirst(tree), []string{"hello", "welcome", "world", "home"}) // true
```

### Other Uses
Feel free to look through the unit tests to see other uses of the tree. There could be some missing use cases. Feel free to submit an issue or add a PR if you want something additional.

# Contact
Tristan Hilbert
tflexsoom\[at\]tflexsoom-dev\[dot\]online