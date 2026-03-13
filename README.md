
# Binary Search Tree - Delete Operation

class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def insert(root, data):
    if root is None:
        return Node(data)
    elif data < root.data:
        root.left = insert(root.left, data)
    else:
        root.right = insert(root.right, data)
    return root

def minValueNode(node):
    current = node
    while current.left is not None:
        current = current.left
    return current

def deleteNode(root, key):
    if root is None:
        return root

    if key < root.data:
        root.left = deleteNode(root.left, key)

    elif key > root.data:
        root.right = deleteNode(root.right, key)

    else:
        if root.left is None:
            temp = root.right
            root = None
            return temp

        elif root.right is None:
            temp = root.left
            root = None
            return temp

        temp = minValueNode(root.right)
        root.data = temp.data
        root.right = deleteNode(root.right, temp.data)

    return root

def inorder(root):
    if root:
        inorder(root.left)
        print root.data,
        inorder(root.right)

root = None

n = int(raw_input("Enter number of nodes: "))
for i in range(n):
    x = int(raw_input("Enter value: "))
    root = insert(root, x)

key = int(raw_input("Enter value to delete: "))
root = deleteNode(root, key)

print "Inorder traversal after deletion:"
inorder(root)


OUTPUT 

Enter number of nodes: 5
Enter value: 50
Enter value: 30
Enter value: 70
Enter value: 20
Enter value: 40
Enter value to delete: 30

Inorder traversal after deletion:
20 40 50 70
