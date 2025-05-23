#  Insert Nodes in a B-Tree

## Aim
To define a Python function `def insert(self, k):` to insert keys into a B-Tree node, ensuring that the tree remains balanced after each insertion.

## Procedure
1. Define a B-Tree node class with keys, children, and a flag to check if it's a leaf.
2. Implement the `insert()` method in the B-Tree class to insert a key `k`.
3. Handle node splitting when a node becomes full during insertion.
4. Maintain the B-Tree properties: balanced and sorted multi-way tree.

## Python Program
```python
# Searching a key on a B-tree in Python


# Create a node
class BTreeNode:
  def __init__(self, leaf=False):
    self.leaf = leaf
    self.keys = []
    self.child = []


# Tree
class BTree:
  def __init__(self, t):
    self.root = BTreeNode(True)
    self.t = t

    # Insert node
  def insert(self, k):
    root = self.root
    if len(root.keys) == (2 * self.t) - 1:
      temp = BTreeNode()
      self.root = temp
      temp.child.insert(0, root)
      self.split_child(temp, 0)
      self.insert_non_full(temp, k)
    else:
      self.insert_non_full(root, k)

    # Insert nonfull
  def insert_non_full(self, x, k):
    i = len(x.keys) - 1
    if x.leaf:
      x.keys.append((None, None))
      while i >= 0 and k[0] < x.keys[i][0]:
        x.keys[i + 1] = x.keys[i]
        i -= 1
      x.keys[i + 1] = k
    else:
      while i >= 0 and k[0] < x.keys[i][0]:
        i -= 1
      i += 1
      if len(x.child[i].keys) == (2 * self.t) - 1:
        self.split_child(x, i)
        if k[0] > x.keys[i][0]:
          i += 1
      self.insert_non_full(x.child[i], k)

    # Split the child
  def split_child(self, x, i):
    t = self.t
    y = x.child[i]
    z = BTreeNode(y.leaf)
    x.child.insert(i + 1, z)
    x.keys.insert(i, y.keys[t - 1])
    z.keys = y.keys[t: (2 * t) - 1]
    y.keys = y.keys[0: t - 1]
    if not y.leaf:
      z.child = y.child[t: 2 * t]
      y.child = y.child[0: t - 1]

  # Print the tree
  def print_tree(self, x, l=0):
    print("Level ", l, " ", len(x.keys), end=":")
    for i in x.keys:
      print(i, end=" ")
    print()
    l += 1
    if len(x.child) > 0:
      for i in x.child:
        self.print_tree(i, l)

  

def main():
  B = BTree(3)

  for i in range(10):
    B.insert((i, 2 * i))
  print("B Tree :")
  B.print_tree(B.root)
  B.insert((11,))
  print("\nB Tree after insertion")
  B.print_tree(B.root)

if __name__ == '__main__':
  main()
```
# Output:
![image](https://github.com/user-attachments/assets/4f355080-dfe2-4afb-b575-331d09abf918)

# Result:
Thus the program successfully completed and The nodes are inserted correctly into the B-Tree while maintaining its properties, and splitting is handled automatically when a node overflows.
