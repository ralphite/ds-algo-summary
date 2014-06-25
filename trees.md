# Trees in Java

> Ralph

##Generic Tree

###Definition

```java
class TreeNode<T> {
    T data;
    Set<TreeNode<T>> children;
}
```

###ADT

```java
interface Tree<T> {
    void insert(T t);
    void remove(T t);
}
```

###Left-child Right-sibling representation

```java
class LcrsTreeNode<T> {
    T data;
    LcrsTreeNode<T> firstChild, nextSibling;
}
```

*which is a binary tree*

> Why? No container required for children => Space Efficient


##Binary Tree

```java
class BinaryTreeNode<T> {
    T data;
    BinaryTreeNode<T> left, right;
}
```

### 

##BST

> node.left.data <= node.data < node.right.data

```java
class BstNode<T extends Comparable<? super T>> {
    T data;
    BstNode<T> left, right;
}
```

###BST methods implementation

```java

// for simplicity duplicates not allowed

public class BST<T extends Comparable<? super T>> {
    private BstNode<T> root;

    public void insert(T t) {
        root = insert(t, root);
    }

    private BstNode<T> insert(T t, BstNode<T> node) {
        if (node == null) return new BstNode<T>(t, null, null);
        int cmp = t.compareTo(node.data);
        if (cmp < 0)
            node.left = insert(t, node.left);
        else if (cmp > 0)
            node.right = insert(t, node.right);
        return node;
    }

    public void remove(T t) {
        root = remove(t, root);
    }

    private BstNode<T> remove(T t, BstNode<T> node) {
        if (node == null) return null;
        int cmp = t.compareTo(node.data);
        if (cmp < 0)
            node.left = remove(t, node.left);
        else if (cmp > 0)
            node.right = remove(t, node.right);
        else {
            if (node.left != null && node.right != null) {
                BstNode<T> rightMin = node.right;
                while (rightMin.left != null)
                    rightMin = rightMin.left;
                node.data = rightMin.data;
                node.right = remove(node.data, node.right);
            } else
                node = node.left != null ? node.left : node.right;
        }
        return node;
    }

    private static class BstNode<T> {
        T data;
        BstNode<T> left, right;

        BstNode(T t, BstNode<T> l, BstNode<T> r) {
            data = t;
            left = l;
            right = r;
        }
    }
}
```

> What's the problem with the code about?
>
> 1. Scan twice to remove
> 2. Unbalanced tree over time
>   - remove leftMax and rightMin alternately
>   - remove leftMax and rightMin randomly

##Traversals

###Recursive

####Pre-order

```python
def preorder(node):
    if node is None:
        return
    visit(node)
    preorder(node.left)
    preorder(node.right)
```

####Post-order

```python
def postorder(node):
    if node is None:
        return
    postorder(node.left)
    postorder(node.right)
    visit(node)
```

####In-order (for binary trees)

```python
def inorder(node):
    if node is None:
        return
    inorder(node.left)
    visit(node)
    inorder(node.right)
```



###Iterative

####Pre-order

```java
public void preorder(BinaryTreeNode<T> node) {
    if(node == null) return;
    ArrayDeque<BinaryTreeNode<T>> stack = new ArrayDeque<BinaryTreeNode<T>>();
    stack.push(node);
    while(!stack.isEmpty()) {
        BinaryTreeNode<T> n = stack.pop();
        visit(n);
        if(n.right!=null)
            stack.push(n.right);
        if(n.left!=null)
            stack.push(n.left);
    }
}
```

####In-order

```java
public void inorder(BinaryTreeNode<T> node) {
    ArrayDeque<BianryTreeNode<T>> stack = new ArrayDeque<BinaryTreeNode<T>>();
    while(node!=null || !stack.isEmpty()) {
        if(node != null) {
            stack.push(node);
            node=node.left;
        } else {
            node = stak.pop();
            visit(node);
            node = node.right;
        }
    }
}
```

####Post-order

```java
public void postorder(BinaryTreeNode<T> node) {
    ArrayDeque<BinaryTreeNode<T>> stack = new ArrayDeque<BinaryTreeNode<T>>();
    BinaryTreeNode<T> prevVisited = null;
    while(node != null || !stack.isEmpty()) {
        if(node != null) {
            stack.push(node);
            node = node.left;
        } else {
            BinaryTreeNode<T> n = stack.peek();
            if(n.right!=null && n.right!=prevVisited) {
                node = n.right;
            } else {
                visit(stack.pop());
                prevVisited = n;
            }
        }
    }
}
```

####Level order

```python
from Queue import Queue
def level_order(node):
    if node is None:
        return
    q = Queue()
    q.put(node)
    while not q.empty():
        n=q.get()
        visit(n)
        if n.left is not None:
            q.put(n.left)
        if n.right is not None:
            q.put(n.right)
```

> All the traversals above require log(n) space which can be considerable when the tree is poorly balanced. Two possible ways to solve this problem
>
>    - Maintain a parent pointer in each node (GIST)
>    - Morris traversals using a threaded tree

###Morris Traversal (O(n) Time, O(1) Space)

####Pre-order

####Inorder

####Postorder

##Threaded Binary Trees

###Only left

###Only right

###Both

##Array Storage

##Self balancing BSTs

###AVL

###Splay

###Red-black

###Treap

##B/B-/B+

##Common problems

###Identical Trees

###Mirrored Tree

###Max Path Sum

###Bottom-up level traversal
