# Trees in Java

> Ralph

##General Tree

```java
class TreeNode<T> {
    T data;
    Set<TreeNode<T>> children;
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

##Binary Tree

```java
class BinaryTreeNode<T> {
    T data;
    BinaryTreeNode<T> left, right;
}
```

###Operations?

```java
interface Tree<T> {
    void insert(T t);
    void remove(T t);
    boolean contains(T t);
}
```

##BST

```java
class BstNode<T extends Comparable<? super T>> {
    T data;
    BstNode<T> left, right;
}
```

###BST methods implementation

```java
public class BST<T extends Comparable<? super T>> {
    private static class BstNode<T> {
        T data;
        BstNode<T> left, right;
        BstNode(T t, BstNode<T> l, BstNode<T> r) {
            data=t; left=l; right=r;
        }
    }
    private BstNode<T> root;
    public void insert(T t) {
        root = insert(t, root);
    }
    private BstNode<T> insert(T t, BstNode<T> node) {
        if(node==null) return new BstNode<T>(t, null, null);
        int cmp = t.compareTo(node.data);
        if(cmp<0)
            node.left = insert(t, node.left);
        else if(cmp>0)
            node.right = insert(t, node.right);
        return node;
    }
    public void remove(T t) {
        root = remove(t, root);
    }
    private BstNode<T> remove(T t, BstNode<T> node) {
        if(node==null) return null;
        int cmp=t.compareTo(node.data);
        if(cmp<0)
            node.left=remove(t, node.left);
        else if (cmp>0)
            node.right = remove(t, node.right);
        else {
            if(node.left!=null && node.right!=null) {
                BstNode<T> rightMin=node.right;
                while(rightMin.left!=null)
                    rightMin=rightMin.left;
                node.data=rightMin.data;
                node.right=remove(node.data, node.right);
            } else 
                node = node.left!=null?node.left:node.right;
        }
        return node;
    }
}
```

##Self balancing BSTs

###AVL

###Splay

###Red-black

###Treap

##B/B-/B+

##Traversals

###Recursive

####Pre-order

####Post-order

####In-order (for binary trees)

####Level order

###Non-recursive

###O(1) space traversals?

##Threaded Binary Trees

###Only left

###Only right

###Both

##Common problems

###Identical Trees

###Mirrored Tree

###Max Path Sum
