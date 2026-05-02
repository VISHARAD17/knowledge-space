---
title: Queue 
---

## 1. Generate Numbers with Given Digits

**Problem:** Generate first n numbers in increasing order using only given digits.

**Input:** n = 10, digits = {5, 6}  
**Output:** `5 6 55 56 65 66 555 556 565 566`

**Explanation:**  
Use BFS approach with a queue. Start with single digits, then generate new numbers by appending each digit to existing numbers.

**Code:**
```java
import java.util.*;

class Solution {
    public void generateNumbers(int n, Set<Integer> digits) {
        Queue<Integer> queue = new LinkedList<>();
        
        for (int digit : digits) {
            queue.offer(digit);
        }
        
        int count = 0;
        while (count < n) {
            int current = queue.poll();
            System.out.print(current + " ");
            count++;
            
            for (int digit : digits) {
                int newNumber = current * 10 + digit;
                queue.offer(newNumber);
            }
        }
    }
}
```

**Code Explanation:**  
Initialize queue with single digits. For each number, print it and generate new numbers by appending each digit. This ensures numbers are generated in increasing order. Time complexity: O(n).

---

## 2. Reverse a Queue

**Problem:** Reverse all elements in a queue.

**Input:** `[10, 5, 15, 20]`  
**Output:** `[20, 15, 5, 10]`

**Explanation:**  
Use a stack to reverse the queue. Pop all elements from queue to stack, then pop from stack back to queue.

**Code:**
```java
import java.util.*;

class Solution {
    public void reverseQueue(Queue<Integer> queue) {
        Stack<Integer> stack = new Stack<>();
        
        while (!queue.isEmpty()) {
            stack.push(queue.poll());
        }
        
        while (!stack.isEmpty()) {
            queue.offer(stack.pop());
        }
    }
}
```

**Code Explanation:**  
Stack's LIFO property reverses the FIFO order of queue. Transfer all elements to stack, then back to queue. Time complexity: O(n), Space: O(n).

---

## Queue Basics

### Queue Operations

**Core Operations:**
```java
Queue<Integer> queue = new LinkedList<>();

// Enqueue (add to rear)
queue.offer(10);  // Returns true/false
queue.add(20);    // Throws exception if fails

// Dequeue (remove from front)
int element = queue.poll();  // Returns null if empty
int element = queue.remove(); // Throws exception if empty

// Peek (view front without removing)
int front = queue.peek();    // Returns null if empty
int front = queue.element(); // Throws exception if empty

// Check if empty
boolean isEmpty = queue.isEmpty();

// Get size
int size = queue.size();
```

### Queue Implementation Types

**1. LinkedList-based Queue:**
```java
Queue<Integer> queue = new LinkedList<>();
```
- Dynamic size
- O(1) enqueue and dequeue
- More memory overhead

**2. ArrayDeque (Recommended):**
```java
Queue<Integer> queue = new ArrayDeque<>();
```
- Faster than LinkedList
- Resizable array
- No capacity restrictions

**3. PriorityQueue:**
```java
Queue<Integer> pq = new PriorityQueue<>();
```
- Elements ordered by priority
- O(log n) enqueue/dequeue
- Not FIFO order

### Common Queue Patterns

**1. Level Order Traversal (BFS):**
```java
void bfs(Node root) {
    Queue<Node> queue = new LinkedList<>();
    queue.offer(root);
    
    while (!queue.isEmpty()) {
        Node current = queue.poll();
        System.out.print(current.data + " ");
        
        if (current.left != null) queue.offer(current.left);
        if (current.right != null) queue.offer(current.right);
    }
}
```

**2. Sliding Window Maximum:**
```java
int[] maxSlidingWindow(int[] nums, int k) {
    Deque<Integer> deque = new ArrayDeque<>();
    int[] result = new int[nums.length - k + 1];
    
    for (int i = 0; i < nums.length; i++) {
        // Remove elements outside window
        while (!deque.isEmpty() && deque.peek() < i - k + 1) {
            deque.poll();
        }
        
        // Remove smaller elements
        while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
            deque.pollLast();
        }
        
        deque.offer(i);
        
        if (i >= k - 1) {
            result[i - k + 1] = nums[deque.peek()];
        }
    }
    return result;
}
```

**3. First Non-Repeating Character in Stream:**
```java
class FirstNonRepeating {
    Queue<Character> queue = new LinkedList<>();
    int[] count = new int[26];
    
    void add(char ch) {
        queue.offer(ch);
        count[ch - 'a']++;
        
        while (!queue.isEmpty() && count[queue.peek() - 'a'] > 1) {
            queue.poll();
        }
    }
    
    char getFirstNonRepeating() {
        return queue.isEmpty() ? '#' : queue.peek();
    }
}
```

### Queue vs Stack

| Feature | Queue | Stack |
|---------|-------|-------|
| Order | FIFO (First In First Out) | LIFO (Last In First Out) |
| Operations | enqueue, dequeue | push, pop |
| Use Cases | BFS, scheduling, buffering | DFS, recursion, undo/redo |
| Real World | Line at store, printer queue | Browser back button, function calls |

### Time Complexity

| Operation | LinkedList | ArrayDeque | PriorityQueue |
|-----------|-----------|------------|---------------|
| Enqueue | O(1) | O(1) amortized | O(log n) |
| Dequeue | O(1) | O(1) | O(log n) |
| Peek | O(1) | O(1) | O(1) |
| Search | O(n) | O(n) | O(n) |

---
