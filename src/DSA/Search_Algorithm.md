# Search Algorithms

# **Binary Search Tree**

**Question:** How would you create a binary search tree?

**Answer:**

to create a tree you need a node. a node in a tree looks like

```jsx
function Node(val){
  this.value = val;
  this.left = null;
  this.right = null;
}

```

Create a constructor for binary search tree

```jsx
function BinarySearchTree(){
  this.root = null;
}

```

Now you need to understand the structure of a binary search tree. For every node value in the left is smaller than the value of the node and value at the right is higher than the value of the root.

so while inserting a value you have to find the appropriate location

```jsx

BinarySearchTree.prototype.push = function(val){
   var root = this.root;

   if(!root){
      this.root = new Node(val);
      return;
   }

   var currentNode = root;
   var newNode = new Node(val);

   while(currentNode){
      if(val < currentNode.value){
          if(!currentNode.left){
             currentNode.left = newNode;
             break;
          }
          else{
             currentNode = currentNode.left;
        }
     }
     else{
         if(!currentNode.right){
            currentNode.right = newNode;
            break;
         }
         else{
            currentNode = currentNode.right;
         }
     }
  }

}

```

```jsx
var bst = new BinarySearchTree();
bst.push(3);
bst.push(2);
bst.push(4);
bst.push(1);
bst.push(5);

```

# **Breadth First Search**

**Question:** How do you implement Breadth First Search

**Answer:**

```

```

ref: [stackoverflow](http://stackoverflow.com/a/13633354/1535443)

ref: [js algorithms](https://github.com/duereg/js-algorithms)

# **Depth first search**

**Question:** How to perform in order traversal

```jsx
function dfs(node){
  if(node){
    console.log(node.value);
    dfs(node.left);
    dfs(node.right);
  }
}

```

# **In order Traversal**

**Question:**

**Answer:**

![https://khan4019.github.io/front-end-Interview-Questions/images/inorder.jpg](https://khan4019.github.io/front-end-Interview-Questions/images/inorder.jpg)

```jsx
function inorder(node){
   if(node){
      inorder(node.left);
      console.log(node.value);
      inorder(node.right);
   }
}

```

ref: [source of image](http://www.javabeat.net/binary-search-tree-traversal-java/)

# **pre order**

![https://khan4019.github.io/front-end-Interview-Questions/images/preorder.jpg](https://khan4019.github.io/front-end-Interview-Questions/images/preorder.jpg)

```jsx
//code here

```

ref: [wiki pseudocode doesnt work for JavaScript](http://en.wikipedia.org/wiki/Tree_traversal)

# **Post order**

![https://khan4019.github.io/front-end-Interview-Questions/images/postorder.jpg](https://khan4019.github.io/front-end-Interview-Questions/images/postorder.jpg)

```jsx
//code here

```

# **min and max value**

**Question:** How can you find the min value in a bst

finding min is super simple. the go through the left node and left most node is the minimum node

```jsx
function minNode(node){
   if(!node){
      return 0;
   }
   if(node.left){
     return minNode(node.left)
  }
  return node.value
}

```

**Question:** How can you find the max value in a bst

```jsx
function maxNode(node){
   if(!node){
     return 0;
  }
  if(node.right){
     return maxNode(node.right)
  }
  return node.value;
}

```

# **Balanced and Unbalanced Tree**

**Question:**What is balanced and unbalanced tree

**Answer:**

1. The left and right subtrees' heights differ by at most one, AND
2. The left subtree is balanced, AND
3. The right subtree is balanced

ref: [Get answer from here](http://stackoverflow.com/questions/8015630/definition-of-a-balanced-tree)

# **Check BST**

**Question:** check a binary tree is BST or not?

**Answer:**

### **Simple but wrong approach**

**Step-1:** if node is null, its BST

```jsx
function isBST(node){
   if(!node){
     return true;
  }

  if(node.left != null && node.left.value > node.value){
    return false;
  }

  if(node.right !=null && node.right.value < node.value) {
    return false;
  }

  if(!isBST(node.left) || !isBST(node.right)) {
    return false;
  }

  return true;
}

```

The reason this method will generate wrong result is for

![https://khan4019.github.io/front-end-Interview-Questions/images/bstWrong.gif](https://khan4019.github.io/front-end-Interview-Questions/images/bstWrong.gif)

### **do in order traversal**

```jsx
//use method 4 in the link below

```

ref: [taken from geeksforgeeks](http://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/)

# **Check balanced**

**Quetion:** How could you check a tree is balanced or not

**Answer:**

check multiple example whether it is balanced. [check balanced tree example](http://webdocs.cs.ualberta.ca/~holte/T26/balanced-trees.html)

ref: [get the answer from here](http://www.geeksforgeeks.org/how-to-determine-if-a-binary-tree-is-balanced/)

# **Height of a tree**

```jsx
function height(node){
   if(!node) return 0;
   var leftHeight = height(node.left);
   var rightHeight = height(node.right);

   return Math.max(leftHeight, rightHeight) + 1;
}

```

# **print ancestor**

**Question:**

**Answer:**

```jsx
function printAncestor(node, target){
   if(!node) return false

   if(node.value == target) return true;

   if(printAncestor(node.left, target) || printAncestor(node.rigth, target)){
     console.log(node.value);
     return true;
  }

  return false
}

```

ref: [from stack overflow](http://stackoverflow.com/questions/12052192/printing-ancestors-of-a-node-in-binary-tree)

# **Doesnt work for intermediate nodes. Debug this**

# **Print all nodes between two nodes**

**Question:**

**Answer:**

```jsx
//put the code

```

ref: [Get the code form here](http://www.geeksforgeeks.org/given-binary-tree-print-nodes-two-given-level-numbers/)

# **common ancestor**

this will work for bst only. If you are dealing with binary tree..this needs to be modified

### **Make this code better**

```jsx
function commonAncestor(node, n1, n2){
   if(!node) return;
   var val = node.value;
   if(n1 < val && n2<val){
     return commonAncestor(node.left, n1, n2);
   }
   if(n1<val && n2<val){
     return commonAncestor(node.right, n1, n2);
  }
  console.log('lowest common ancestor value: ', val);
  return node;
}

```

ref: [common ancesotr](http://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-search-tree/)

### **coomon ancestor for binary tree**

```jsx
function commonAncestorBT(node, n1, n2){
   if(!node) return;
   var val = node.value;
   if(n1 == val || n2 ==val){
     return node;
   }
   var left = commonAncestorBT(node.left, n1, n2);
   var right = commonAncestorBT(node.right, n1, n2);
   if(left && right){
     return node;
  }
  return (left) ? left : right;
}

```

ref: [try pavels blog](http://www.fusu.us/2013/06/p2-lowest-common-ancestor-in-binary-tree.html)

ref: [common ancestor for binary tree](http://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)

# **check bst is height balanced**

**Qustion**

ref: [get code from here](http://www.geeksforgeeks.org/how-to-determine-if-a-binary-tree-is-balanced/)

# **Top view**

# **bottom view**

# **leftview**

ref: [bst left view](http://www.geeksforgeeks.org/print-left-view-binary-tree/)

# **Right view**

ref: [print right view](http://www.geeksforgeeks.org/print-right-view-binary-tree-2/)

# **Merge two BST**

ref: [merge two bst](http://www.geeksforgeeks.org/merge-two-bsts-with-limited-extra-space/)

# **convert binary to BST**

ref: [binary tree to bst](http://www.geeksforgeeks.org/binary-tree-to-binary-search-tree-conversion/)

# **Check Sub tree**

ref: [check subtree](http://www.geeksforgeeks.org/check-binary-tree-subtree-another-binary-tree-set-2/)

# **Diagonal Sum**

ref: [gfg](http://www.geeksforgeeks.org/diagonal-sum-binary-tree/)

# **Self Balancing or Height Balanced Tree**

**Question:**

**Answer:**

A binary tree whose height of the left subtree and height of the right subtree differ at most one.

# **AVL Tree**

**Question:**

**Answer:**

It is Self balancing binary search tree. This means in an AVL tree, heights of two child subtrees of any node differ by at most one. If at any time if heights differ more than one, re-balancing is done to restore the height balance property.

Lookup, insertion and deletion all takes O(logn) in average and worst case

# **Insert, delete Into AVL**

# **Red Black Tree**

**Question:**

**Answer:**A red-black tree is a binary search tree with one extra attribute for each node: the colour, which is either red or black.

- Every node is either red or black.
- Every leaf (NULL) is black.
- If a node is red, then both its children are black. However, two black node may be adjacent
- Every simple path from a node to a descendant leaf contains the same number of black nodes.
- Root node will always be black

![https://khan4019.github.io/front-end-Interview-Questions/images/rb_tree1a.gif](https://khan4019.github.io/front-end-Interview-Questions/images/rb_tree1a.gif)

ref: [Red Black Trees](https://www.cs.auckland.ac.nz/software/AlgAnim/red_black.html)

# **Insert into Red Black Tree**