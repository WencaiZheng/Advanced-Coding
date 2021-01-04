# Data Basic

**1 byte** is group of 8 **bits**

| Type                                                   | Size        |
| ------------------------------------------------------ | ----------- |
| bool, char, unsigned char, signed char, __int8         | 1 **byte**  |
| __int16, short, unsigned short, wchar_t, __wchar_t     | 2 **bytes** |
| float, __int32, int, unsigned int, long, unsigned long | 4 **bytes** |
| **double**, __int64, long **double**, long long        | 8 **bytes** |

# Tree

## Binary Search Tree

### Balance Search Tree

Guaranteed height of log(n) when n items present 

#### Red Black Tree

Decolor,rotation

For hash tables (like dicts or sets), insertion and lookup are O(1), while for a balanced tree these are O(log(n)). In-order traversal of keys is O(n) in a tree, but to do the same thing with a hash table you need to sort the keys first, so it's O(n*log(n))

1. Root and NIL leaves are always black
2. If node is red, its children are black
3. All path from a node to Null leave have the same black nodes
4. Longest path are no more than twice the length of the shortest

```PYTHON

```

# Linked list

Array is not good at deleting and adding (O(N)) because it has continuous memory space, while it is good at searching.

Linked list becomes available as a result. Linked list can be seen as a 'one-branch' binary tree. It has O(1) adding and deleting.

