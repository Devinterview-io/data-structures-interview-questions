# Top 100 Data Structures Interview Questions

<div>
<p align="center">
<a href="https://devinterview.io/questions/data-structures-and-algorithms/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fdata-structures-and-algorithms-github-img.jpg?alt=media&token=fa19cf0c-ed41-4954-ae0d-d4533b071bc6" alt="data-structures-and-algorithms" width="100%">
</a>
</p>

#### You can also find all 100 answers here 👉 [Devinterview.io - Data Structures](https://devinterview.io/questions/data-structures-and-algorithms/data-structures-interview-questions)

<br>

## 1. Explain how you would reverse an array in place.

**In-place reversal** modifies the original array without extra space.

Here is a general-purpose implementation:

### Code Example: Array Reversal

Here is the Python code:

```python
def reverse_array(arr):
    start, end = 0, len(arr) - 1
    while start < end:
        arr[start], arr[end] = arr[end], arr[start]
        start, end = start + 1, end - 1
        
my_array = [1, 2, 3, 4, 5]
print("Original Array:", my_array)
reverse_array(my_array)
print("Reversed Array:", my_array)
```
<br>

## 2. What is the difference between an _array_ and a _linked list_?

Let me put the two fundamental type of lists,  **Arrays** and **Linked Lists**, into perspective.

### Key Distinctions

#### Data Organization

* **Array**: Employs sequential memory storage and each element has a unique index.
* **Linked List**: Elements are scattered in memory and accessed sequentially via references (pointers).

#### Memory Management

* **Array**: Typically requires a single, contiguous memory block.
* **Linked List**: Memory allocations are dynamic and non-contiguous.

#### Complexity Analysis

| Operation     | Array     | Linked List |
| ------------- |-----------| ------------|
| Access        | $O(1)$ (with index)  | $O(n)$ |
| Bulk Insertion| $O(n)$ or $O(1)$  | $O(1)$ |
| Deletion      | $O(n)$ to $O(1)$   | $O(1)$ |

### When to Use Each

- **Arrays** are preferable when:
  - There's a need for direct or random access such as in lookup tables.
  - The data will remain relatively unchanged, and performance in accessing elements takes precedence over frequent insertions or deletions.

- **Linked Lists** are more suitable when:
  - Frequent insertions and deletions are expected, especially in the middle.
  - The exact size of the list isn't known in advance, and you want the memory to be used flexibly.
  - The primary operations are sequential, such as iteration from the beginning to the end.

### Code Example: Array vs. Linked List

Here is the Python code:

#### Array
```python
# Define array
my_array = [10, 20, 30, 40, 50]

# Access element by index
print(my_array[2])  # Output: 30

# Bulk insertion at the beginning
my_array = [5, 6, 7] + my_array
print(my_array)  # Output: [5, 6, 7, 10, 20, 30, 40, 50]

# Deletion from the middle
del my_array[4]
print(my_array)  # Output: [5, 6, 7, 10, 30, 40, 50]
```

#### Linked List
```python
# Define linked list nodes (in reality, you'd have a LinkedList class)
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Create linked list
head = Node(10)
node1 = Node(20)
node2 = Node(30)
head.next = node1
node1.next = node2

# Bulk insertion at the beginning
new_node1 = Node(5)
new_node2 = Node(6)
new_node3 = Node(7)
new_node3.next = head
head = new_node1
new_node1.next = new_node2
print_nodes(head)  # Output: 5, 6, 7, 10, 20, 30

# Deletion from the middle
new_node1.next = new_node3
# Now, just print_nodes(head) will output: 5, 6, 7, 20, 30
```
<br>

## 3. How would you check for duplicates in an array without using extra space?

**Checking for duplicates** in an array without additional space is a common challenge with solutions using hash functions, sorting, and mathematical calculations.

### Brute Force Method

The code checks for duplicates based on numerical repetition.

#### Complexity Analysis

- **Time Complexity**: $O(n^2)$
- **Space Complexity**: $O(1)$

#### Code Implementation

Here is the Python code:

```python
def has_duplicates(arr):
    n = len(arr)
    for i in range(n):
        for j in range(i+1, n):
            if arr[i] == arr[j]:
                return True
    return False

arr = [1, 2, 3, 4, 3]
print(has_duplicates(arr))  # Output: True
```

### Sorting Approach

This method involves sorting the array using a **comparison-based sorting algorithm** like Quick Sort. If two adjacent elements are the same, then the array has duplicates.

#### Complexity Analysis

- **Time Complexity**: Best/Worst: $O(n \log n)$
- **Space Complexity**: $O(1)$ or $O(n)$ depending on sorting algorithm

#### Code Implementation

Here is the Python code:

```python
def has_duplicates_sorted(arr):
    arr.sort()
    n = len(arr)
    for i in range(n - 1):
        if arr[i] == arr[i+1]:
            return True
    return False

arr = [1, 2, 3, 4, 3]
print(has_duplicates_sorted(arr))  # Output: True
```

### Mathematical Approach

For this method, **the sum of numbers in the array** is calculated. Mathematically, if no duplicates are present, the sum of consecutive natural numbers can be calculated to compare against the actual sum.

If $\text{actual sum} - \text{sum of numbers in the array} = 0$, there are no duplicates.

#### Code Implementation

Here is the Python code:

```python
def has_duplicates_math(arr):
    array_sum = sum(arr)
    n = len(arr)
    expected_sum = (n * (n-1)) // 2  # Sum of first (n-1) natural numbers
    return array_sum - expected_sum != 0

arr = [1, 2, 3, 4, 5, 5]
print(has_duplicates_math(arr))  # Output: True
```
<br>

## 4. Can you explain how to perform a _binary search_ on a sorted array?

Let's look at the high-level **strategy** behind binary search and then walk through a **step-by-step example**.

### Binary Search Strategy

1. **Divide & Conquer**: Begin with the entire sorted array and refine the search range in each step.
2. **Comparison**: Use the middle element to determine the next search range.
3. **Repetition**: Continue dividing the array until the target is found or the search range is empty.

### Step-by-Step Example

Let's consider the following array with the target value of `17`:

```plaintext
[1, 3, 6, 7, 9, 12, 15, 17, 20, 21]
```

1. **Initial Pointers**: We start with the whole array.  
   ```plaintext
   [1, 3, 6, 7, 9, 12, 15, 17, 20, 21]  
   ^                               ^
   Low                             High
   Middle: (Low + High) / 2 = 5
   ```

   This identifies the `Middle` number as `12`.

2. **Comparison**: Since the `Middle` number is less than the target `17`, we can **discard** the left portion of the array.
   ```plaintext
   [15, 17, 20, 21]
   ^           ^
   Low        High
   ```

3. **Updated Pointers**: We now have a reduced array to search.
   ```plaintext
   Middle = 7
   ^      ^
   Low   High
   ```

4. **Final Comparison**:  
   Since the `Middle` number is now the target, `17`, the search is successfully concluded.
<br>

## 5. How would you rotate a two-dimensional _array_ by 90 degrees?

Rotating a 2D array by $90^\circ$ can be visually understood as a **transpose** followed by a **reversal** of rows or columns.

### Algorithm: Transpose and Reverse

1. **Transpose**: Swap each element $A[i][j]$ with its counterpart $A[j][i]$
2. **Reverse Rows (for $90^\circ$ CW)** or Columns (for $90^\circ$ CCW)

### Complexity Analysis

- **Time Complexity**: Both steps run in $O(n^2)$ time.
- **Space Complexity**: Since we do an in-place rotation, it's $O(1)$.

#### Code Example: Matrix Rotation

Here is the Python code:

```python
def rotate_2d_clockwise(matrix):
    n = len(matrix)
    # Transpose
    for i in range(n):
        for j in range(i, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    # Reverse Rows
    for i in range(n):
        for j in range(n//2):
            matrix[i][j], matrix[i][n-j-1] = matrix[i][n-j-1], matrix[i][j]

    return matrix

def rotate_matrix_ccw(matrix):
    n = len(matrix)
    # Transpose
    for i in range(n):
        for j in range(i, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    # Reverse Columns
    for i in range(n):
        for j in range(n//2):
            matrix[j][i], matrix[n-j-1][i] = matrix[n-j-1][i], matrix[j][i]

    return matrix

# Test 
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(rotate_2d_clockwise(matrix))
# Output: [[7, 4, 1], [8, 5, 2], [9, 6, 3]]
```
<br>

## 6. Describe an algorithm to compress a string such as "_aabbccc_" to "_a2b2c3_".

You can compress a string following the count of each character. For example, "_aabbccc_" becomes "_a2b2c3_".

The python code for this algorithm is:

```python
def compress_string(input_string):
    # Initialize
    current_char = input_string[0]
    char_count = 1
    output = current_char

    # Iterate through the string
    for char in input_string[1:]:
        # If the character matches the current one, increment count
        if char == current_char:
            char_count += 1
        else:  # Append the count to the output and reset for the new character
            output += str(char_count) + char
            current_char = char
            char_count = 1

    # Append the last character's count
    output += str(char_count)

    # If the compressed string is shorter than the original string, return it
    return output if len(output) < len(input_string) else input_string
```

### Time Complexity

This algorithm has a time complexity of $O(n)$ since it processes each character of the input string exactly once.

### Space Complexity

The space complexity is $O(k)$, where $k$ is the length of the compressed string. This is because the **output** string is stored in memory.
<br>

## 7. What is an _array slice_ and how is it implemented in programming languages?

Let's look at what is an **Array Slice** and how it's implemented in some programming languages.

### What is an Array Slice?

An array slice is a view on an existing array that acts as a smaller array. The slice references a continuous section of the original array which allows for efficient data access and manipulation.

Array slices are commonly used in languages like **Python**, **Rust**, and **Go**.

### Key Operations

- **Read**: Access elements in the slice.
- **Write**: Modify elements within the slice.
- **Grow/Shrink**: Resize the slice, often DWARF amortized.
- **Iteration**: Iterate over the elements in the slice.

### Underlying Mechanism

A slice typically contains:

1. A **pointer** to the start of the slice.
2. The **length** of the slice (the number of elements in the slice).
3. The **capacity** of the slice (the maximum number of elements that the slice can hold).

#### Benefit of Use

- **No Copy Overhead**: Slices don't duplicate the underlying data; they're just references. This makes them efficient and memory-friendly.
- **Flexibility**: Slices can adapt as the array changes in size.
- **Safety**: Languages like **Rust** use slices for enforcing safety measures, preventing out-of-bounds access and memory issues.

### Popular Implementations

- **Python**: Uses list slicing, with syntax like `my_list[2:5]`. This creates a new list.
  
- **Go Lang**: Employs slices extensively and is perhaps the most slice-oriented language out there.

- **Rust**: Similar to Go, it's a language heavily focused on memory safety, and slices are fundamental in that regard.

### Code Example: Array Slicing

Here is the **Python** code:

  ```python
  original_list = [1, 2, 3, 4, 5]
  my_slice = original_list[1:4]  # Creates a new list: [2, 3, 4]
  ```
  
  Here is the **Rust** code:

  ```rust
  let original_vec = vec![1, 2, 3, 4, 5];
  let my_slice = &original_vec[1..4];  // References a slice: [2, 3, 4]
  ```

  And here is the **Go** code:

  ```go
  originalArray := [5]int{1, 2, 3, 4, 5}
  mySlice := originalArray[1:4]  // References the originalArray from index 1 to 3
  ```
<br>

## 8. Can you discuss the _time complexity_ of _array insertion_ and _deletion_?

Both **array insertions** and **deletions** have a time complexity of $O(n)$ due to potential need for data re-arrangement.

### Array Insertion

- **Beginning**: $O(n)$ if array full; $1$ for shifting.
- **Middle**: $O(n)$ to make room and insert.
- **End**: $O(1)$ on average for appending.

### Array Deletion

- **Beginning**: $O(n)$ due to re-arrangement often needed.
- **Middle**: $O(n)$ as it involves shifting.
- **End**: $O(1)$ for most cases, but $O(n)$ when dynamic resizing is required.
<br>

## 9. What are some ways to merge two sorted _arrays_ into one sorted _array_?

Merging two sorted arrays into a new sorted array can be accomplished through a variety of well-established techniques.

### Methods of Merging Sorted Arrays

1. **Using Additional Space**: 
    - Create a new array and add elements from both arrays using two pointers, then return the merged list.
    - Time Complexity: $O(n + m)$ - where $n$ and $m$ are the number of elements in each array. This approach is simple and intuitive.

2. **Using a Min Heap**:
   - Select the smallest element from both arrays using a min-heap and insert it into the new array.
   - Time Complexity: $O((n + m) \log (n + m))$ 
   - Space Complexity: $O(n + m)$ - Heap might contain all the elements.
   - This approach is useful when the arrays are too large to fit in memory.

3. **In-Place Merge**:
    - Implement a merge similar to the one used in **Merge Sort**, directly within the input array.
    - Time Complexity: $O(n \cdot m)$ - where $n$ and $m$ are the number of elements in each array.
    - **In-Place Merging** becomes inefficient as the number of insertions increases.

4. **Using Binary Search**: 
   - Keep dividing the larger array into two parts and using binary search to find the correct position for elements in the smaller array.
   - Time Complexity: $O(m \log n)$

5. **Two-Pointer Technique**:
   - Initialize two pointers, one for each array, and compare them to determine the next element in the merged array.
   - Time Complexity: $O(n + m)$
<br>

## 10. How do you find the _kth largest element_ in an unsorted _array_?

To find the $k^{\text{th}}$ largest element in an unsorted array, you can **leverage heaps or quicksort**.

### Quickselect Algorithm

- **Idea**: Partition the array using a pivot (similar to quicksort) and divide into subarrays until the partitioning index is the $k^{\text{th}}$ largest element.

- **Time Complexity**: 
  - Worst-case: $O(n^2)$ - This occurs when we're faced with the least optimized scenario, reducing $n$ by only one element for each stitch step.
  - Average-case: $O(n)$ - Average performance is fast, making the expected time complexity linear.
  
- **Code Example**: Python

  ```python
  import random
  
  def quickselect(arr, k):
      if arr:
          pivot = random.choice(arr)
          left = [x for x in arr if x < pivot]
          right = [x for x in arr if x > pivot]
          equal = [x for x in arr if x == pivot]
          if k < len(left):
              return quickselect(left, k)
          elif k < len(left) + len(equal):
              return pivot
          else:
              return quickselect(right, k - len(left) - len(equal))
  ```

### Heap Method

- Build a **max-heap** $O(n)$ - This takes linear time, making $O(n) + O(k \log n) = O(n + k \log n)$.
- Extract the max element $k$ times (each time re-heapifying the remaining elements).

### Code Example: Python 

```python
import heapq

def kth_largest_heap(arr, k):
    if k > len(arr): return None
    neg_nums = [-i for i in arr]
    heapq.heapify(neg_nums)
    k_largest = [heapq.heappop(neg_nums) for _ in range(k)]
    return -k_largest[-1]
```
<br>

## 11. Explain how a _singly linked list_ differs from a _doubly linked list_.

**Singly linked lists** and **doubly linked lists** differ in how they manage node-to-node relationships.

### Structure

- **Singly Linked List**: Each node points to the next node.

- **Doubly Linked List**: Both previous and next nodes are pointed to.

### Visual Representation

#### Singly Linked List

![Singly Linked List](https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/linked-lists%2Fsingly-linked-list.svg?alt=media&token=c6e2ad4f-e2d4-4977-a215-6253e71b6040)

#### Doubly Linked List

![Doubly Linked List](https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/linked-lists%2Fdoubly-linked-list.svg?alt=media&token=5e14dad3-c42a-43aa-99ff-940ab1d9cc3d)

### Key Distinctions

- **Access Direction**: Singly linked lists facilitate one-way traversal, while doubly linked lists support bi-directional traversal.

- **Head and Tail Movements**: Singly linked lists only operate on the head, while doubly linked lists can manipulate the head and tail.

- **Backward Traversal Efficiency**: Due to their structure, singly linked lists may be less efficient for backward traversal.

- **Memory Requirement**: Doubly linked lists use more memory as each node carries an extra pointer.

### Code Example: Singly Linked List

Here is the Java code:

```java
public class SinglyLinkedList {
    
    private static class Node {
        private int data;
        private Node next;

        public Node(int data) {
            this.data = data;
            this.next = null;
        }
    }

    private Node head;

    public void insertFirst(int data) {
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
    }

    public void display() {
        Node current = head;
        while (current != null) {
            System.out.println(current.data);
            current = current.next;
        }
    }
}
```

### Code Example: Doubly Linked List

Here is the Java code:

```java
public class DoublyLinkedList {
    
    private static class Node {
        private int data;
        private Node previous;
        private Node next;

        public Node(int data) {
            this.data = data;
            this.previous = null;
            this.next = null;
        }
    }

    private Node head;
    private Node tail;

    public void insertFirst(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            tail = newNode;
        } else {
            head.previous = newNode;
            newNode.next = head;
            head = newNode;
        }
    }

    public void display() {
        Node current = head;
        while (current != null) {
            System.out.println(current.data);
            current = current.next;
        }
    }

    public void displayBackward() {
        Node current = tail;
        while (current != null) {
            System.out.println(current.data);
            current = current.previous;
        }
    }
}
```
<br>

## 12. How would you detect a _cycle_ in a _linked list_?

**Cycle detection** in a linked list is a fundamental algorithm that uses pointers to identify if a linked list has a repeating sequence.

### Floyd's "Tortoise and Hare" Algorithm

Floyd's algorithm utilizes two pointers:

- The "tortoise" moves one step each iteration.
- The "hare" moves two steps.

If the linked list does not have a cycle, the hare either reaches the end (or null) before the tortoise, or vice versa. However, if there is a cycle, the two pointers **are guaranteed to meet** inside the cycle.

### Algorithm Steps

1. Initialize both pointers to the start of the linked list.
2. Move the tortoise one step and the hare two steps.
3. Continuously advance the pointers in their respective steps:
   - If the tortoise reaches the hare (a collision point), return such a point.
   - If either pointer reaches the end (null), conclude there is no cycle.

### Visual Representation

![Floyd's Algorithm](https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/data%20structures%2Ffloyd-warshall-algorithm.png?alt=media&token=edbf8bd3-979a-44e8-ad49-041e9f30cece)

### Complexity Analysis

- **Time Complexity**: $O(n)$ where $n$ is the number of nodes in the linked list, due to each pointer visiting each node only once.
- **Space Complexity**: $O(1)$ as the algorithm uses only a constant amount of extra space.

### Code Example: Floyd's Cycle Detection

Here is the Python code:

```python
def has_cycle(head):
    tortoise = head
    hare = head

    while hare and hare.next:
        tortoise = tortoise.next
        hare = hare.next.next

        if tortoise == hare:
            return True

    return False
```
<br>

## 13. What are the major operations you can perform on a _linked list_, and their _time complexities_?

Let's look at the major operations you can perform on a **singly linked list** and their associated time complexities:

### Operations & Time Complexities

#### Access (Read/Write) $O(n)$

- **Head**: Constant time: $O(1)$.
- **Tail**: $O(n)$ without a tail pointer, but constant with a tail pointer.
- **Middle or k-th Element**: $\frac{n}{2}$ is around the middle node; getting k-th element requires $O(k)$.

#### Search $O(n)$

- **Unordered**: May require scanning the entire list. Worst case: $O(n)$.
- **Ordered**: You can stop as soon as the value exceeds what you're looking for.

#### Insertion $O(1)$ without tail pointer, $O(n)$ with tail pointer

- **Head**: $O(1)$
- **Tail**: $O(1)$ with a tail pointer, otherwise $O(n)$.
- **Middle**: $O(1)$ with tail pointer and finding position in $O(1)$ time; otherwise, it's $O(n)$.

#### Deletion $O(1)$ for Head and Tail, $O(n)$ otherwise

- **Head**: $O(1)$
- **Tail**: $O(n)$ because you must find the node before the tail for pointer reversal with a single pass.
- **Middle**: $O(n)$ since you need to find the node before the one to be deleted.

#### Length $O(n)$

- **Naive**: Requires a full traversal. Every addition or removal requires this traversal.
- **Keep Count**: Maintain a separate counter, updating it with each addition or removal.

### Code Example: Singly Linked List Basic Operations

Here is the Python code:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None
    
    def append(self, data):  # O(n) without tail pointer
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        last_node = self.head
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
    
    def delete(self, data):  # O(n) only if element is not at head
        current_node = self.head
        if current_node.data == data:
            self.head = current_node.next
            current_node = None
            return
        while current_node:
            if current_node.data == data:
                break
            prev = current_node
            current_node = current_node.next
        if current_node is None:
            return
        prev.next = current_node.next
        current_node = None

    def get_middle(self):  # O(n)
        slow, fast = self.head, self.head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow

    def get_kth(self, k):  # O(k)
        current_node, count = self.head, 0
        while current_node:
            count += 1
            if count == k:
                return current_node
            current_node = current_node.next
        return None

    # Other methods: display, length, etc.
```
<br>

## 14. Can you describe an _in-place algorithm_ to reverse a _linked list_?

**In-Place Algorithms** modify data structures with a constant amount of extra working space $O(1)$.

A **Singly Linked List** presents a straightforward example of an in-place data structure, well-suited for in-place reversal algorithms.

### Reversing a Linked List: Core Concept

The reversal algorithm just needs to update each node's `next` reference so that they point to the previous node. A few key steps achieve this:

1. **Initialize**: Keep track of the three key nodes: `previous`, `current`, and `next`.
2. **Reverse Links**: Update each node to instead point to the previous one in line.
3. **Move Pointers**: Shift `previous`, `current`, and `next` nodes by one position for the next iteration. 

This process proceeds iteratively until `current` reaches the end, i.e., `NULL`.

### Complexity Analysis

- **Time Complexity**: The algorithm exhibits a linear time complexity of $O(n)$ as it visits each node once.
- **Space Complexity**: As the algorithm operates in-place, only a constant amount of extra space (for nodes pointers) is required: $O(1)$.

### Code Example: In-Place List Reversal

Here is the Python code:

```python
class Node:
    def __init__(self, data=None):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        last_node = self.head
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node

    def reverse_inplace(self):
        previous = None
        current = self.head
        while current:
            next_node = current.next
            current.next = previous
            previous = current
            current = next_node
        self.head = previous

    def display(self):
        elements = []
        current = self.head
        while current:
            elements.append(current.data)
            current = current.next
        print(" -> ".join(str(data) for data in elements))

# Populate the linked list
llist = LinkedList()
values = [4, 2, 8, 3, 1, 9]
for value in values:
    llist.append(value)

# Display original
print("Original Linked List:")
llist.display()

# Reverse in-place and display
llist.reverse_inplace()
print("\nAfter Reversal:")
llist.display()
```
<br>

## 15. Explain how you would find the _middle element_ of a _linked list_ in one pass.

**Finding the middle element** of a linked list is a common problem with several efficient approaches, such as the **two-pointer (or "runner") technique**.

### Two-Pointer Technique

#### Explanation

The two-pointer technique uses two pointers, often named `slow` and `fast`, to traverse the list. While `fast` moves two positions at a time, `slow` trails behind, covering a single position per move. When `fast` reaches the end, `slow` will be standing on the middle element.

### Example

Given the linked list: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7

The pointers will traverse as follows:

- (1) `slow`: 1; `fast`: 2
- (2) `slow`: 2; `fast`: 4
- (3) `slow`: 3; `fast`: 6
- (4) `slow`: 4; `fast`: end

At (4), the `slow` pointer has reached the middle point.

### Complexity Analysis

- **Time Complexity**: $O(N)$ -- For every N nodes, we check each node once.
- **Space Complexity**: $O(1)$ -- We only use pointers; no extra data structures are involved.

### Code Example: Two-Pointer (Runner) technique

Here is the Python implementation:

```python
def find_middle_node(head):
    if not head:
        return None

    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```
<br>



#### Explore all 100 answers here 👉 [Devinterview.io - Data Structures](https://devinterview.io/questions/data-structures-and-algorithms/data-structures-interview-questions)

<br>

<a href="https://devinterview.io/questions/data-structures-and-algorithms/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fdata-structures-and-algorithms-github-img.jpg?alt=media&token=fa19cf0c-ed41-4954-ae0d-d4533b071bc6" alt="data-structures-and-algorithms" width="100%">
</a>
</p>

